---
title:  "[C#] Thread and WPF"
excerpt: "Thread, ThreadPools, Tasks, and WPF"

categories:
  - C#

last_modified_at: 2019-12-26T19:00:00
---

## Thread Start and End & Completion
- TaskCompletionSource 클래스를 이용해 Task 생성 후 Thread에서 값 setting 하여야 Task.Result 수행 가능
- Start() 메서드를 이용해 Thread 시작
- 작업이 완료되면 알아서 종료

```c#
taskCompletionSource = new TaskCompletionSource<bool>();

var thread = new Thread(() =>
{
    Console.WriteLine($"Thread Number: {Thread.CurrentThread.ManagedThreadId} started");
    Thread.Sleep(5000);
    taskCompletionSource.TrySetResult(true);
    Console.WriteLine($"Thread Number: {Thread.CurrentThread.ManagedThreadId} ended");
});

thread.Start();

var test = taskCompletionSource.Task.Result;
```
- 생성한 Thread에서 TrySetResult 를 이용해 값 지정
- thread 시작하여 Task 수행하면 Result 이용하여 값 도출


## ThreadPools
- 백그라운드에서 여러가지 작업을 하는 데 사용할 수 있는 thread collection
- 기본 thread에서 다른 작업을 비동기적으로 수행
- 일반적으로 thread 최대 수 지정, 모든 thread에서 작업을 수행중이면, 다른 작업은 사용 한 스레드가 생길 때까지 큐에 배치,
  가능한 스레드가 생기면 자동으로 큐에 배치되었던 스레드 실행

```c#
Enumerable.Range(0, 1000).ToList().ForEach(f =>
{
    ThreadPool.QueueUserWorkItem((o) =>
    {
        Console.WriteLine($"Thread Number: {Thread.CurrentThread.ManagedThreadId} started");
        Thread.Sleep(1000);
        Console.WriteLine($"Thread Number: {Thread.CurrentThread.ManagedThreadId} ended");
    });                
});
```
- 위의 작업을 기본적인 thread 를 생성하여 수행 시, 프로세서 한계에 무관하게 Thread를 계속 만들어 부담
- Threadpool 이용하여 적정한 thread 수 관리


## Join and IsAlive
- Join 메서드가 호출 되는 스레드가 완료될 때까지, 호출 스레드를 차단하는 동기화 방법
- IsAlive 메서드는 현재 스레드의 실행 상태 값을 반환

```c#
private static void ThreadProc()
{
  Console.WriteLine("\nCurrent thread: {0}", Thread.CurrentThread.Name);
  if (Thread.CurrentThread.Name == "Thread1" && 
      thread2.ThreadState != ThreadState.Unstarted)
      thread2.Join();
  
  Thread.Sleep(4000);
  Console.WriteLine("\nCurrent thread: {0}", Thread.CurrentThread.Name);
  Console.WriteLine("Thread1: {0}", thread1.ThreadState);
  Console.WriteLine("Thread2: {0}\n", thread2.ThreadState);
}
```
- Thread1 이 Thread2 의 join 메서드를 호출하여 2가 완료되기 전까지는 1을 차단

## Tasks and WPF
- UI를 제어하기 위해서는 MainThread에 접근 필요
- 즉, 다른 Thread에서 UI 수정 불가
- Dispathcher, Async-Await 등의 방법으로 제어

```c#
private void MyButton_Click(object sender, RoutedEventArgs e)
{
    Task.Run(() =>
    {
        Debug.WriteLine($"Thread #. {Thread.CurrentThread.ManagedThreadId}");
        HttpClient webClient = new HttpClient();
        string html = webClient.GetStringAsync("http://ipv4.download.thinkbroadband.com/20MB.zip").Result;

        MyButton.Dispatcher.Invoke(() =>
        {
            Debug.WriteLine($"Thread #. {Thread.CurrentThread.ManagedThreadId}");
            MyButton.Content = "Done";
        });
    });
}
```
- 버튼 클릭 시 20MB 다운로드
- Task (thread) 사용하지 않을 시, MainThread가 멈추어 다운로드가 모두 끝난 후에 UI제어 가능
- Dispathcer 이용하여 다운로드하는 스레드 안에서 UI 제어

```c#
private async void MyButton_Click2(object sender, RoutedEventArgs e)
{
    string myHtml = "str";

    Debug.WriteLine($"Thread #. {Thread.CurrentThread.ManagedThreadId} before await task");
    await Task.Run(async () =>
    {
        Debug.WriteLine($"Thread #. {Thread.CurrentThread.ManagedThreadId} during await task");
        HttpClient webClient = new HttpClient();
        string html = webClient.GetStringAsync("https://google.com").Result;
        myHtml = html;
    });

    Debug.WriteLine($"Thread #. {Thread.CurrentThread.ManagedThreadId} after wait task");
    MyButton.Content = "Done Downloading";
    MyWebBrowser.SetValue(Htmlproperty, myHtml);
}
```
- 버튼 클릭 시 Web 불러오기
- async-await 이용해서 Task의 작업(download thread) 수행 후 MainThread에서 UI 제어


----
**ref :**  
- [Thread.Join Method](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread.join?view=netframework-4.8)  
- [Asynchronous programming with async and await](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/async/)