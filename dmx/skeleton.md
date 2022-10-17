---
description: Structures and linked data definitions for skeleton
---

# Skeleton

## JSON

```json
{
	"parentIndex" : 0,
	"name" : "bone-000",
	"pos" : {
		"x" : 0,
		"y" : 0,
		"z" : 0
	},
	"rot" : {
		"x" : 0,
		"y" : 0,
		"z" : 0,
		"w" : 1
	},
	"scl" : {
		"x" : 1,
		"y" : 1,
		"z" : 1
	}
}
```

## Binary

### Struct 

```c
typedef struct {
	char name[0x20];
	uint32_t index;
	uint32_t parentIndex;
	DashVec3 pos;
	DashVec4 rot;
	DashVec3 scl;
} DashBone;
```

### Table

| Offset | 0x00 | 0x04 | 0x08 | 0x0c |
| ------ | ------ | ------ | ------ | ------ |
| 0x0010 | name | 0000 | 0000 | 0000 |
| 0x0020 | 0000 | 0000 | 0000 | 0000 |
| 0x0000 | `index` | `parentIndex` | `pos.x` | `pos.y` |
| 0x0030 | `pos.z` | `rot.x` | `rot.y` | `rot.z` |
| 0x0040 | `rot.w` | `scl.x` | `scl.y` | `scl.z` |