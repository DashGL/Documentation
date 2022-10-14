---
description: Describes the format for the texture structure and section
---

# Texture

## JSON

The required fields for the JSON version of the format are `name` and `data`.  Default values will be included for the fields where values are not provided to reduce file size.&#x20;

### Format

```json
{
    "name": "texture_000",
    "flipY": false,
    "width": 256,
    "height": 256,
    "wrapS": 1000,
    "wrapT": 1000,
    "data": "data:image/qoi;base64,..."
}
```

### Type

```typescript
type DashTexture = {
    name: string;
    flipY: boolean | undefined;
    width: number | undefined;
    height: number | undefined;
    wrapS: DashTextureWrap | undefined;
    wrapT: DashTextureWrap | undefined;
    data: string;
}
```

### Fields

#### name

The name of the texture as a string. This field is required. The max length of the string is **31** characters to conform with the binary version of the file format. In cases where images are exported from the file for editing, the images will be assigned these names.&#x20;

Reference: [https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.name](https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.name)

#### flipY

If set to `true`, the texture is flipped along the vertical axis when uploaded to the GPU. If not provided value is assumed to be `true`.&#x20;

Reference: [https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.flipY](https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.flipY).&#x20;

#### width

The width of the image in pixels. This value MUST be an integer that is zero or greater. While this value can be extracted from the image data, it is expected to be present for readability.&#x20;

#### height

The height of the image in pixels. This value MUST be an integer that is zero or greater. While this value can be extracted from the image data, it is expected to be present for readability.&#x20;

#### wrapS

This defines how the texture is wrapped horizontally and corresponds to **U** in UV mapping. The default is `DashTextureWrap.ClampToEdgeWrapping`, where the edge is clamped to the outer edge texels. The other two choices are `DashTextureWrap.RepeatWrapping` and `DashTextureWrap.MirroredRepeatWrapping`.

Reference: [https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.wrapS](https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.wrapS)

#### wrapT

This defines how the texture is wrapped vertically and corresponds to **V** in UV mapping. The default is `DashTextureWrap.ClampToEdgeWrapping`, where the edge is clamped to the outer edge texels. The other two choices are `DashTextureWrap.RepeatWrapping` and `DashTextureWrap.MirroredRepeatWrapping`.

Reference: [https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.wrapT](https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.wrapT)

#### data

The data for the image encoded in the "Quite OK Image Format" as a base64 string starting with the constant value of `data:image/qoi;base64,.`&#x20;

**NOTE**: tiling of images in textures only functions if image dimensions are powers of two (2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, ...) in terms of pixels. Individual dimensions need not be equal, but each must be a power of two. This is a limitation of OpenGL.

Reference: [https://qoiformat.org/](https://qoiformat.org/)

### Enums

```typescript
enum DashTextureWrap {
  RepeatWrapping = 1000,
  ClampToEdgeWrapping = 1001,
  MirroredRepeatWrapping = 1002,
}
```

## Binary

Textures contain the image data used in the model. Because images are not a fixed size, this property section is divided into two parts, and structured similar to an archive.&#x20;

### Struct

```c
typedef struct {
	char name[0x20];
	uint32_t index;
	uint32_t flipY;
	uint32_t width;
	uint32_t height;
	uint32_t wrapS;
	uint32_t wrapT;
	uint32_t byteOffset;
	uint32_t byteLength;
} DashTexture;
```

### Table

| Offset | 0x00  | 0x04  | 0x08       | 0x0c       |
| ------ | ----- | ----- | ---------- | ---------- |
| 0x0000 | name  | 0000  | 0000       | 0000       |
| 0x0010 | 0000  | 0000  | 0000       | 0000       |
| 0x0020 | index | flipY | width      | height     |
| 0x0030 | wrapS | wrapT | byteOffset | byteLength |

### Fields

#### index

The index of the texture in the array starting from zero.&#x20;

Reference: [https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.id](https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.id)

#### name

The name of the texture. This is a zero terminated string value. Such that the last byte in the string must be `0x00`, giving this field a max length of 31 characters and a fixed length of `0x20` bytes.&#x20;

Reference: [https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.name](https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.name)

#### flipY

Is a boolean value defined by `0x00` for `false` and `0x01` for `true`.&#x20;

Reference: [https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.flipY](https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.flipY).&#x20;

#### width

The width of the image in pixels.&#x20;

#### height

The height of the image in pixels.&#x20;

#### wrapS

This defines how the texture is wrapped horizontally and corresponds to **U** in UV mapping. The options are `DASH_TEXTURE_REPEAT_WRAP`, `DASH_TEXTURE_CLAMP_WRAP` and `DASH_TEXTURE_MIRROR_WRAP`.&#x20;

Reference: [https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.wrapS](https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.wrapS)

#### wrapT

This defines how the texture is wrapped vertically and corresponds to **V** in UV mapping. `DASH_TEXTURE_REPEAT_WRAP`, `DASH_TEXTURE_CLAMP_WRAP` and `DASH_TEXTURE_MIRROR_WRAP`.&#x20;

Reference: [https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.wrapT](https://threejs.org/docs/index.html?q=textu#api/en/textures/Texture.wrapT)

#### byteOffset

The absolute byte offset in the file for the start of the image data

#### byteLength

The byte length of the image data encoded in the "Quite OK Image Format".&#x20;

**NOTE**: tiling of images in textures only functions if image dimensions are powers of two (2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, ...) in terms of pixels. Individual dimensions need not be equal, but each must be a power of two. This is a limitation of OpenGL.

Reference: [https://qoiformat.org/](https://qoiformat.org/)

### **Constants**

```
#define DASH_TEXTURE_REPEAT_WRAP 1000 // THREE.RepeatWrapping
#define DASH_TEXTURE_CLAMP_WRAP  1001 // THREE.ClampToEdgeWrapping
#define DASH_TEXTURE_MIRROR_WRAP 1002 // THREE.MirroredRepeatWrapping
```

## Limitations

* `name` field has a limited number of characters
* Only supports diffuse color textures
* Only supports a single image type
