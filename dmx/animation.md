---
description: Structures and linked data definitions for animations
---

# Animation

## JSON

In the JSON format, each animation is decribed with a name and a length in seconds. 
This is paired with a `keyframes` array which provides a list of key frames which
describes a transformation such as position, rotation or scale which will be applied
to a bone at a specific time.

### Format

```json
{
	"name": "idle",
    "duration": 0.5,
    "keyframes" : [{
        "time": 0.1,
        "boneIndex": 0,
        "type": "rotation",
        "x": 0,
        "y": 0,
        "z": 0,
        "w": 1
    }]
}
```

### Type

```typescript
type DashKeyframe = {
    time: number;
	boneIndex: number;
    type: DashKeyFrameType;
    x: number;
    y: number;
    z: number;
    w: number | undefined;
}

type DashAnimation = {
    name: string;
    duration: number;
    keyframes: DashKeyframe[]
}
```

### Terms

#### name

The name of the animation. 

#### duration

The length of the animation in seconds.

#### keyframes

The list of keyframes which describe the animation. 

#### time

The time for the keyframe value.

#### boneIndex

The bone influenced by the keyframe value

#### type

The type of value for the keyframe. Posible values are `position`, `rotation` and `scale`. 
`position` and `scale` require `x`, `y` and `z` values to be set for the keyframe.
`rotation` requires `x`, `y`, `z`, `w` values to be set for the keyframe.

#### x

The `x` axis value of the keyframe.

#### y

The `y` axis value of the keyframe.

#### z

The `z` axis value of the keyframe.

#### w

The `w` axis value of the keyframe.

### Enums

```typescript
enum DashKeyFrameType {
  Position = "position",
  Rotation = "rotation",
  Scale = "scale",
}
```

## Binary

Becuase the length of any animation is not fixed, the Dash Model Exchange format 

### Struct 

```c
typedef struct {
	char name[0x20];
	uint32_t index;
    float duration;
	uint32_t offset;
	uint32_t count;
} DashAnimation;

typedef struct {
	uint32_t index;
    uint32_t boneIndex;
	uint32_t type;
    float time;
    DashVec4 value;
} DashKeyframe;
```

### Table

| Offset | 0x00 | 0x04 | 0x08 | 0x0c |
| ------ | ------ | ------ | ------ | ------ |
| 0x0010 | name | 0000 | 0000 | 0000 |
| 0x0020 | 0000 | 0000 | 0000 | 0000 |
| 0x0000 | `index` | `duration` | `keyFrameOffset` | `count` |


| Offset | 0x00 | 0x04 | 0x08 | 0x0c |
| ------ | ------ | ------ | ------ | ------ |
| 0x0010 | `index` | `boneIndex` | `type` | `time` |
| 0x0020 | `value.x` | `value.y` | `value.z` | `value.w` |

### Fields

### Terms

#### name

The name of the animation. 

#### duration

The length of the animation in seconds.

#### offset

The byte offset of the keyframe list

#### count

The number of entries in the keyframe list.

#### index

The keyframe's index in the array starting from `0`.

#### boneIndex

The bone influenced by the keyframe value

#### type

The type of value for the keyframe. Posible values are `DASH_ANIM_TYPE_POS`, `DASH_ANIM_TYPE_ROT` and `DASH_ANIM_TYPE_SCL`. 
`DASH_ANIM_TYPE_POS` and `DASH_ANIM_TYPE_SCL` require `x`, `y` and `z` values to be set for the keyframe.
`DASH_ANIM_TYPE_ROT` requires `x`, `y`, `z`, `w` values to be set for the keyframe.

#### time

The time for the keyframe value.

#### x

The `x` axis value of the keyframe.

#### y

The `y` axis value of the keyframe.

#### z

The `z` axis value of the keyframe.

#### w

The `w` axis value of the keyframe. Value will be ignored when `type` is not `rotation`. 

### **Constants**

```
#define DASH_ANIM_TYPE_POS 1
#define DASH_ANIM_TYPE_ROT 2 
#define DASH_ANIM_TYPE_SCL 3 
```

## Limitations

* only supports skeletal animation, not texture or material animations
