---
title:  "[Unity] Procedural Mesh (3)"
excerpt: "Cube"

categories:
  - Unity

last_modified_at: 2020-03-11T18:30:00
---

### Requirements for Cube
  - 6 sides = 6 quads
  - Hard edges = quads need their own vertices
  - 24 vertices, but only 8 vertex positions

### Quads 구성을 위한 방식
1. Hard code : 6 quads, vertices 모두 직접 타이핑하여 구현
2. Procedural quads : 모두 자동화하여 빌드시에 구현
3. Goldilocks quads : 최초의 8개의 정점을 하드코딩 후, quad 함수로 triangle 구현

### Vertex 구성 방식
- 오른쪽이 X+, 앞쪽이 Z+, 윗쪽이 Y+

| ![vertex compose](/assets/images/posts/200311/vertex_compose.png) |
|:--:|
| Composition of vertices |

### CubeMeshData
```c#
public static Vector3[] vertices =
{
    new Vector3( 1, 1, 1),
    new Vector3(-1, 1, 1),
    new Vector3(-1,-1, 1),
    new Vector3( 1,-1, 1),
    new Vector3(-1, 1,-1),
    new Vector3( 1, 1,-1),
    new Vector3( 1,-1,-1),
    new Vector3(-1,-1,-1)
};

public static int[][] faceTriangles =
{
    new int[] {0, 1, 2, 3},
    new int[] {5, 0, 3, 6},
    new int[] {4, 5, 6, 7},
    new int[] {1, 4, 7, 2},
    new int[] {5, 4, 1, 0},
    new int[] {3, 2, 7, 6},
};

public static Vector3[] faceVertices(int dir, float scale, Vector3 pos)
{
    Vector3[] fv = new Vector3[4];
    for (int i = 0; i < fv.Length; i++)
    {
        fv[i] = vertices[faceTriangles[dir][i]] * scale + pos;
    }

    return fv;
}
```
- 정점(vertex) 8개를 하드코딩
- 각 면(face) 6개에 해당하는 정점 정의
- 각 면에 대한 정점 값 불러오는 함수 정의


### Procedural cube
```c#
void MakeCube(float cubeScale, Vector3 cubePos)
{
    vertices = new List<Vector3>();
    triangles = new List<int>();

    for (int i = 0; i < 6; i++)
    {
        MakeFace(i, cubeScale, cubePos);
    }
}

void MakeFace(int dir, float faceScale, Vector3 facePos)
{
    vertices.AddRange(CubeMeshData.faceVertices(dir, faceScale, facePos));
    int vCount = vertices.Count;

    triangles.Add(vCount - 4);
    triangles.Add(vCount - 4 + 1);
    triangles.Add(vCount - 4 + 2);
    triangles.Add(vCount - 4);
    triangles.Add(vCount - 4 + 2);
    triangles.Add(vCount - 4 + 3);
}
```
- 각 면에 대한 triangle 2개를 구현하는 함수
- 각 면에 대한 vertex가 4개씩 추가되기 때문에 (vCount - 4) 적용

----
**ref**  
[Procedural Mesh Tutorial, Part 8: Cube Basics](https://www.youtube.com/watch?v=bnmr_At2R0s)  
