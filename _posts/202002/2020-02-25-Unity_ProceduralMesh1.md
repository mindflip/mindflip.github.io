---
title:  "[Unity] Procedural Mesh (1)"
excerpt: "Mesh Basics"

categories:
  - Unity

last_modified_at: 2020-02-25T18:30:00
---

정밀맵 데이터(shapefile)를 이용해, Unity에서 3D 지도를 구현해야하는 일이 필요하여 알아보았다.

### Procedural generation 
  - 직접 데이터를 생산하는 것이 아닌, 특정한 알고리즘을 통해 자동적/자율적으로 생산하는 것

### Rendering
- 3차원 공간에 물체를 배치하고, 이를 모니터 화면에 나타내는 작업
- 순서 : 메쉬정보 구축(Mesh Filter) -> 재질 설정(Mesh Renderer) -> 카메라 설정(Transform)

### Mesh
- 물체를 3차원으로 표현하기 위한 점(Vertex), 선(Edge), 면(Polygon)의 모음
- 유니티에서는 크게 정점(Vertex)과 삼각면(Triangle Face)로 구성
- 정점 집합 : Vector3[] vertices
  - Mesh에게 points 위치를 알려줌
- 삼각면 집합 : int[] triangles
  - Mesh에게 triangle 만들기 위한 순서 집합을 알려줌(3 indices로 구분)

![Mesh triangles](/assets/images/posts/200225/mesh_triangles.png)

### Mesh Components
- **`Mesh Filter`** : 에셋에서 메쉬를 취득해, 화면상에서 렌더링하기 위해 Mesh Renderer에 전달
- **`Mesh Renderer`** : 메쉬 필터 지오메트리를 사용해, 오브젝트의 Transform 컴포넌트에서 정의된 위치에 렌더링

### Ex Source Code
```c#
[RequireComponent(typeof(MeshFilter))]
[RequireComponent(typeof(MeshRenderer))]
public class ProceduralMesh : MonoBehaviour
{
    Mesh mesh;

    Vector3[] vertices;
    int[] triangles;

    private void Awake()
    {
        mesh = GetComponent<MeshFilter>().mesh;
    }

    void Start()
    {
        MakeMeshData();
        CreateMesh();
    }

    void MakeMeshData()
    {
        // create an array of vertices
        vertices = new Vector3[] { new Vector3(0, 0, 0), new Vector3(0, 0, 1), new Vector3(1, 0, 0), new Vector3(1,0,1) };
        // create an array of integers
        triangles = new int[] { 0, 1, 2, 2, 1, 3 };
    }

    void CreateMesh()
    {
        mesh.Clear();
        mesh.vertices = vertices;
        mesh.triangles = triangles;
    }
}
```
- MeshFilter, MeshRenderer 컴포넌트를 오브젝트에 자동등록
- 정점 4개를 이용해 사각형 구성 -> triangle 2개 필요
- triangle을 이루는 정점 순서를 clockwise로 구성
- mesh를 밑에서 관찰할 때는, counter-clockwise 상태이며 rendering 하지 않음
  - Back-face culling (관찰자가 볼 수 없는 면은 그리지 않음)

| ![Mesh quad implementation](/assets/images/posts/200225/mesh_quad1.png) | ![Clockwise order of vertices](/assets/images/posts/200225/triangle_order0.gif) |
|:--:|:--:|
| Clockwise ordering of vertices | Back-face culling |


----
**ref**  
[Procedural Mesh Tutorial, Part 1: Mesh Basics](https://www.youtube.com/watch?v=ucuOVL7c5Hw)  
[[Unity] Rendering 렌더링 - Texture , Mesh , Material](https://blog.naver.com/PostView.nhn?blogId=winterwolfs&logNo=10180058416&proxyReferer=https%3A%2F%2Fwww.google.com%2F)