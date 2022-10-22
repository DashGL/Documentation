---
description: Structures and linked data definitions for faces
---

# Face

The `Face` array defines the list of faces for the mesh. Each face defines a material index,
which gives the face its color properties based on material defined from the material list.
Faces are all trianges and define `a`, `b`, `c` indices from the vertex list for the position.

Each vertex can additionally be provided with `color`, `normals` and `uv`. The reason that 
these are defined here and not in the vertex list, is because the vertex list is intended to
be a unique list of positions associated with weight. The attributes of `color`, `normals`, 
and `uv` define properties of a face-per-point. And as such were included in the face
definition for the purposes of defining an interchange format. 

In the case of a delivery format, these properties would be declared in the vertex list.

## JSON

### Format

```json
{
  "material": 0,
  "a": {
    "index": 0,
    "color": "rgb(255, 255, 255)",
    "normal": [0, 0, 0],
    "uv": [0, 0]
  },
  "b": {
    "index": 0,
    "color": "rgb(255, 255, 255)",
    "normal": [0, 0, 0],
    "uv": [0, 0]
  },
  "c": {
    "index": 0,
    "color": "rgb(255, 255, 255)",
    "normal": [0, 0, 0],
    "uv": [0, 0]
  }
}
```

### Type

```typescript
type DashPoint = {
  index: number;
  color: string | undefined;
  normal: number[],
  uv: number[] | undefined;
}

type DashFace = {
  material: number;
  a: DashPoint;
  b: DashPoint;
  c: DashPoint;
}
```

### Fields

#### material

The index of the material to use for the face.

#### a

The `a` point for the triangular face

#### b

The `b` point for the triangular face

#### c

The `c` point for the triangular face

#### index

The index of the vertex from the vertex list which describes the position for the point.

#### normal

The normal value for the vertex as a vec3. 

#### color

The color for the vertex as an 8 byte rgba value. 

#### uv

The diffuse texture mapping for the vertex as vec2. A texture must be assigned 
to the material for the face to this to have any effect. 


## Binary

### Struct

```c
typedef struct {
  uint32_t index;
  uint8_t color[4];
  float normal[3];
  float uv[2];
} DashPoint;

typedef struct {
  uint32_t index;
  uint32_t material;
  DashPoint a;
  DashPoint b;
  DashPoint c;
} DashFace;
```

### Table


| Offset | 0x00  | 0x04  | 0x08       | 0x0c       |
| ------ | ----- | ----- | ---------- | ---------- |
| 0x0000 | index | material | a.index | a.color |
| 0x0010 | a.normal[0] | a.normal[1] | a.normal[2] | a.uv[0] |
| 0x0020 | a.uv[1] | b.index | b.color | b.normal[0] |
| 0x0030 | b.normal[1] | b.normal[2] | b.uv[0] | b.uv[1] |
| 0x0040 | c.index | c.color | c.normal[0] | c.normal[1] |
| 0x0050 | c.normal[2] | c.uv[0] | c.uv[1] |  |

### Fields

#### index

The index of the face in the array starting from zero.

#### material

The index of the material to use for the face.

#### a

The `a` point for the triangular face

#### b

The `b` point for the triangular face

#### c

The `c` point for the triangular face

#### index

The index of the vertex from the vertex list which describes the position for the point.

#### normal

The normal value for the vertex as a vec3. 

#### color

The color for the vertex as an 8 byte rgba value. 

#### uv

The diffuse texture mapping for the vertex as vec2. A texture must be assigned 
to the material for the face to this to have any effect. 


## Limiations

- Should we be using `{ x, y, z }` and `{ u, v }` structs?
- We have a `nop` at the end of the face struct
- Should we move normals, color and uv to the vertex definition?
- Do we want to allow for nested types in our definition?