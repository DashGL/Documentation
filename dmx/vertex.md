# Vertex

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

#### x

The x-axis coordinate for a given vertex.

Reference: [https://threejs.org/docs/#api/en/math/Vector3.x](https://threejs.org/docs/#api/en/math/Vector3.x)

#### y

The y-axis coordinate for a given vertex.&#x20;

Reference: [https://threejs.org/docs/#api/en/math/Vector3.y](https://threejs.org/docs/#api/en/math/Vector3.y)

#### z

The z-axis coordinate for a given vertex.

Reference: [https://threejs.org/docs/#api/en/math/Vector3.z](https://threejs.org/docs/#api/en/math/Vector3.z)

#### skinIndex

The index of the bones which influence this vertex. Expected format is an array of integers with a length of four or less. `skinWeight` must also be defined for this to have any effect.

In this case in which the defined vertex does not require skinning, this field does not need to be defined.&#x20;

Default: `[0,0,0,0]`

#### skinWeight

The weight for which each bone influences the vertex. Expected format is an array of floats that equals the array length of `skinIndex`. Foreach index a float between 0 and 1 is expected to assign the weight of which bone transformations are to be applied to the vertex.&#x20;

Default: `[0,0,0,0]`

## Binary

### Struct

```c
typedef struct {
  uint32_t index;
  float x;
  float y;
  float z;
  uint32_t skinIndex[4];
  float skinWeight[4];
} DashVertex;
```

### Table


| Offset | 0x00  | 0x04  | 0x08       | 0x0c       |
| ------ | ----- | ----- | ---------- | ---------- |
| 0x0000 | index  | x  | y       | z       |
| 0x0010 | skinIndex[0]  | skinIndex[1]  | skinIndex[2] | skinIndex[3] |
| 0x0020 | skinWeight[0] | skinWeight[1] | skinWeight[2] | skinWeight[3] |

### Fields

#### x

The x-axis coordinate for a given vertex.

Default: `0.0f`

Reference: [https://threejs.org/docs/#api/en/math/Vector3.x](https://threejs.org/docs/#api/en/math/Vector3.x)

#### y

The y-axis coordinate for a given vertex.&#x20;

Default: `0.0f`

Reference: [https://threejs.org/docs/#api/en/math/Vector3.y](https://threejs.org/docs/#api/en/math/Vector3.y)

#### z

The z-axis coordinate for a given vertex.

Default: `0.0f`

Reference: [https://threejs.org/docs/#api/en/math/Vector3.z](https://threejs.org/docs/#api/en/math/Vector3.z)

#### skinIndex

The index of the bones which influence this vertex. Expected format is an array of integers with a length of four or less. `skinWeight` must also be defined for this to have any effect.

In this case in which the defined vertex does not require skinning, this field does not need to be defined.&#x20;

Default: `{ 0,0,0,0 }`

#### skinWeight

The weight for which each bone influences the vertex. Expected format is an array of floats that equals the array length of `skinIndex`. Foreach index a float between 0 and 1 is expected to assign the weight of which bone transformations are to be applied to the vertex.&#x20;

Default: `{ 0.0f, 0.0f, 0.0f, 0.0f }`

## Limiations

- `skinIndex` and `skinWeight` add a lot of space for non-skinned meshes
- do we want to declare a way to toggle between skinned and non-skinned meshes for the file type?