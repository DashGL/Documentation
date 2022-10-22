---
description: Structures and linked data definitions for skeleton
---

# Skeleton

The bone structure contains the local transformation for the bone defined. This is done by provided a `vec3` for the
position and scale, and a `vec4` for the rotation. The local matrix and world matrix are then calulated from these
values.

## JSON

```json
{
	"parentIndex": 0,
	"name" : "bone-000",
	"position" : {
		"x" : 0,
		"y" : 0,
		"z" : 0
	},
	"rotation" : {
		"x" : 0,
		"y" : 0,
		"z" : 0,
		"w" : 1
	},
	"scale" : {
		"x" : 1,
		"y" : 1,
		"z" : 1
	}
}
```

### Type

```typescript
type DashBone = {
	name: string;
	parentIndex: number | null | undefined;
	position: DashVec3 | undefined;
	rotation: DashVec4 | undefined;
	scale: DashVec3 | undefined;
}
```

### Terms

#### parentIndex

The parent index of the bone by position in the array. Bones should be organized in the array such that 
the root bone comes are index 0 and child bones are defined after their parent bones. A `null` value
for this field indicates their is no parent bone, implying the root bone.

Default: `null`

#### name

The name of the bone, such as `shoulder`, `neck`, `knee` to define the functionality of which connection
the bone is intended to represent.

No default value is generated for this field onload.

#### position

The local position for the bone relative to its parent. 

Default: `{ x: 0, y: 0, z: 0 }`

#### rotation

The local rotation for the bone relative to its parent.

Default: `{ x: 0, y: 0, z: 0, w: 1 }`

#### scale

The scale value for the bone.

Default: `{ x: 1, y: 1, z: 1 }`

## Binary

### Struct 

```c
typedef struct {
	char name[0x20];
	uint32_t index;
	uint32_t parentIndex;
	DashVec3 position;
	DashVec4 rotation;
	DashVec3 scale;
} DashBone;
```

### Table

| Offset | 0x00 | 0x04 | 0x08 | 0x0c |
| ------ | ------ | ------ | ------ | ------ |
| 0x0010 | name | 0000 | 0000 | 0000 |
| 0x0020 | 0000 | 0000 | 0000 | 0000 |
| 0x0000 | `index` | `parentIndex` | `position.x` | `position.y` |
| 0x0030 | `position.z` | `rotation.x` | `rotation.y` | `rotation.z` |
| 0x0040 | `rotation.w` | `scale.x` | `scale.y` | `scale.z` |

### Fields

#### name

The name of the bone, such as `shoulder`, `neck`, `knee` to define the functionality of which connection
the bone is intended to represent.

No default value is generated for this field onload.

#### parentIndex

The parent index of the bone by position in the array. Bones should be organized in the array such that 
the root bone comes are index 0 and child bones are defined after their parent bones. As the root
bone does not have a parent, this value will be ignored for the first element in the array.

Default: `0`

#### position

The local position for the bone relative to its parent. 

Default: `{ 0.0f, 0.0f, 0.0f }`

#### rotation

The local rotation for the bone relative to its parent.

Default: `{ 0.0f, 0.0f, 0.0f, 1.0f }`

#### scale

The scale value for the bone.

Default: `{ 1.0f, 1.0f, 1.0f }`