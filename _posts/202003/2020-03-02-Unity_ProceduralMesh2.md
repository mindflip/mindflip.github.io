---
title:  "[Unity] Procedural Mesh (2)"
excerpt: "Procedural Grid"

categories:
  - Unity

last_modified_at: 2020-03-02T18:30:00
---

### Common Procedural Meshes 
  - Grids
  - Cubes (Voxels)
  - Extrusions

### Grids
- 2차원 공간의 정점 배열을 이용하여  
Quads, Triangles, Hexagons 등과 같은 planes cells를 형성

### Grid parameter
- Cell size
- Cell position
- Grid position
- Cell count

### Discrete Cells Ex
```c#
void MakeDiscreteProceduralGrid()
    {
        // set array sizes
        vertices = new Vector3[gridSize * gridSize * 4];
        triangles = new int[gridSize * gridSize * 6];

        // set tracker integers
        int v = 0;
        int t = 0;

        // set vertex offset
        float vertexOffset = cellSize * 0.5f;

        for(int x = 0; x < gridSize; x++)
        {
            for(int y = 0; y < gridSize; y++)
            {
                Vector3 cellOffset = new Vector3(x * cellSize, 0, y * cellSize);

                // populate the vertices and triangles arrays
                vertices[v] = new Vector3(-vertexOffset, 0, -vertexOffset) + cellOffset + gridOffset;
                vertices[v + 1] = new Vector3(-vertexOffset, 0, vertexOffset) + cellOffset + gridOffset;
                vertices[v + 2] = new Vector3(vertexOffset, 0, -vertexOffset) + cellOffset + gridOffset;
                vertices[v + 3] = new Vector3(vertexOffset, 0, vertexOffset) + cellOffset + gridOffset;
                // if you put 'x+y' to y value in the vectors, you can check distinct quads that are not sharing their vertices

                triangles[t] = v;
                triangles[t + 1] = triangles[t + 4] = v + 1;
                triangles[t + 2] = triangles[t + 3] = v + 2;
                triangles[t + 5] = v + 3;

                v += 4;
                t += 6;
            }
        }
    }
```
- quads를 구성하는 정점(vertex)이 따로 설정되어 cell 마다 독립적
- grid size만큼의 가로세로에 정점 4개를 이용
- 반복문 이용해 vertices, triangles 할당

### Contiguous Cells Ex
```c#
    void MakeContiguousProceduralGrid()
    {
        // set array sizes
        vertices = new Vector3[(gridSize + 1) * (gridSize + 1)];
        triangles = new int[gridSize * gridSize * 6];

        // set tracker integers
        int v = 0;
        int t = 0;

        // set vertex offset
        float vertexOffset = cellSize * 0.5f;

        // create vertex grid
        for (int x = 0; x <= gridSize; x++)
        {
            for (int y = 0; y <= gridSize; y++)
            {
                vertices[v] = new Vector3((x * cellSize) - vertexOffset, (x+y)*0.2f, (y * cellSize) - vertexOffset);
                v++;
            }
        }

        // reset vertex tracker
        v = 0;

        // setting each cell's triangles
        for (int x = 0; x < gridSize; x++)
        {
            for (int y = 0; y < gridSize; y++)
            {
                triangles[t] = v;
                triangles[t + 1] = triangles[t + 3] = v + 1;
                triangles[t + 2] = triangles[t + 5] = v + (gridSize + 1);
                triangles[t + 4] = v + (gridSize + 1) + 1;

                v++;
                t += 6;
            }
            v++;
        }
    }
```
- quads를 구성하는 정점(vertex)을 공유
- 가로세로 정점의 갯수는 grid size + 1
- 반복문을 통해 vertices, triangles 할당



| ![Discrete cells](/assets/images/posts/200302/discrete_cells.png) | ![Contiguous cells](/assets/images/posts/200302/contiguous_cells.png) |
|:--:|:--:|
| Discrete cells | Contiguous cells |

----
**ref**  
[Procedural Mesh Tutorial, Part 6: Procedural Grid (Discrete Cells)](https://www.youtube.com/watch?v=8PlpCbxB6tY)  
