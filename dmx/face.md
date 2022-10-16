---
description: Structures and linked data definitions for faces
---

# Face

## JSON

### Format

```json
{
	"x": 0,
	"y": 0,
	"z": 0,
	"skinIndex": [0,0,0,0],
	"skinWeight": [0,0,0,0]
}
```

### Type

```typescript
type DashVertex = {
	x: number,
	y: number,
	z: number,
	skinIndex: number[] | undefined;
	skinWeight: number[] | undefined;
}
```

### Fields


## Binary

### Struct

```c
typedef struct {
  uint32_t index;
  uint32_t materialIndex;
  uint32_t visible;
  uint32_t a;
  uint32_t b;
  uint32_t c;
  uint8_t aVertecColor[4];
  uint8_t bVertecColor[4];
  uint8_t cVertecColor[4];
  float aNrm[3];
  float bNrm[3];
  float cNrm[3];
  float aUv[2];
  float bUv[2];
  float cUv[2];
} DashFace;
```

### Table


| Offset | 0x00  | 0x04  | 0x08       | 0x0c       |
| ------ | ----- | ----- | ---------- | ---------- |
| 0x0000 | index | materialIndex | a | b |
| 0x0010 | c | aNrm[0] | aNrm[1] | aNrm[2] |
| 0x0020 | bNrm[0] | bNrm[1] | bNrm[2] | cNrm[0] |
| 0x0030 | cNrm[1] | cNrm[2] | aUv[0] | aUv[1] |
| 0x0040 | bUv[0] | bUv[1] | cUv[0] | cUv[1] |
| 0x0050 | aVertecColor | bVertexColor | cVertexColor |  |

### Fields

#### index

The index of the face in the array starting from zero.

#### materialIndex

The index of the material to use for the face.

#### a

The `a` vertex index for the triangular face

#### b

The `b` vertex index for the triangular face

#### c

The `c` vertex index for the triangular face

#### aNrm

The normal value for the `a` vertex as a vec3.

#### bNrm

The normal value for the `b` vertex as a vec3.

#### cNrm

The normal value for the `c` vertex as a vec3.

#### aUv

The diffuse texture mapping for the `a` vertex as vec2. A texture must be assigned 
to the material for the face to this to have any effect. 

#### bUv

The diffuse texture mapping for the `b` vertex as vec2. A texture must be assigned 
to the material for the face to this to have any effect. 

#### cUv

The diffuse texture mapping for the `c` vertex as vec2. A texture must be assigned 
to the material for the face to this to have any effect. 

## Limiations

- Should we be using `{ x, y, z}` and `{ u, v }` structs?
- We have a `nop` at the end of the face struct
- Should we move normals, color and uv to the vertex definition?