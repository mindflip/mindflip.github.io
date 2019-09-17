---
title:  "[Andorid] Fragment"
excerpt: "안드로이드 프래그먼트"

categories:
  - Android

last_modified_at: 2019-09-17T18:30:00
---

프래그먼트는 액티비티에 위치할 수 있는 UI 조각  
프래그먼트와 상호작용은 `FragmentManager`를 통해 수행

### Creating a Fragment
![fragment_lifecycle](/assets/images/posts/190917/fragment_lifecycle.png)

- Activity와 클래스 코드가 많이 닮아있음(similar callback method)
- `onCreate()`
  - 프래그먼트 첫 생성시 호출. 컴포넌트 초기화 담당.
- `onCreateView()`
  - 프래그먼트가 화면에 그려질 때 호출. 그려낼 UI가 있으면 View return. 아니면 null return.
- `onPause()`
  - 사용자가 프래그먼트를 떠나는 첫 알림으로 호출. 변화가 있으면 이 메서드에서 commit 해줘야함.

### Adding a user interface
프래그먼트는 액티비티의 ui로 사용되고, 독자적인 레이아웃으로 액티비티에 포함  
레이아웃을 제공하기 위해 `onCreateView()` 구현 필요

```java
public static class ExampleFragment extends Fragment {
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.example_fragment, container, false);
    }
}
```
- XML에 정의된 레이아웃을 inflate 시켜 return
- inflate은 3가지 파라미터 (resource ID, ViewGroup, boolean indicating whether the inflated layout should be attached to the ViewGroup)

### Adding a fragment to an activity
2가지 방법 존재
- 레이아웃 파일 안에 프래그먼트 선언

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <fragment android:name="com.example.news.ArticleListFragment"
            android:id="@+id/list"
            android:layout_weight="1"
            android:layout_width="0dp"
            android:layout_height="match_parent" />
    <fragment android:name="com.example.news.ArticleReaderFragment"
            android:id="@+id/viewer"
            android:layout_weight="2"
            android:layout_width="0dp"
            android:layout_height="match_parent" />
</LinearLayout>
```

- 존재하는 ViewGroup에 프래그먼트 추가

```java
FragmentManager fragmentManager = getSupportFragmentManager();
FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
```
이후에 `add()` 메서드를 이용해 프래그먼트 추가
```java
ExampleFragment fragment = new ExampleFragment();
fragmentTransaction.add(R.id.fragment_container, fragment);
fragmentTransaction.commit();
```






----
**ref :**  
[android developer docs - Fragment](https://developer.android.com/guide/components/fragments)  