---
description: Structures and linked data definitions for materials
---

# Material

## Json

The only required field for `Materials` is the `name`. All other fields will provide default values if not provided.

### Format

```json
{
	"name" : "material-000",
	"transparent": false,
	"alphaTest": 0,
	"visible": true,
	"color": "rgb(255,255,255)",
	"map": null,
	"renderSide": "front",
	"vertexColor" : true,
	"blending" : "custom",
	"blendEquation" : "additive",
	"blendSrc" : "srcAlphaFactor",
	"blendDst" : "oneMinusSrcAlphaFactor",
	"emissive": "rgb(0,0,0)",
	"emissiveIntensity": 1,
	"specularColor": "rgb(0,0,0)",
	"shininess": 30,
	"shaderType": "basic",
	"opacity": 1
}
```

### Type

```typescript
type DashMatrial = {
    name: string;
    transparent: boolean | undefined;
    alphaTest: number | undefined;
    visible: boolean | undefined;
    color: string | undefined;
    map: number | null | undefined;
    renderSide: DashMaterialSide | undefined;
    shadowSide: DashMaterialSide | undefined;
    vertexColor: boolean | undefined;
    blending: DashBlending | undefined;
    blendEquation: DashBlendingEquations | undefined;
    blendSrc: DashSourceFactors | undefined;
    blendDst: DashSourceFactors | undefined;
    emissiveColor: string | undefined;
    emissiveIntensity: number | undefined;
    specular: string | undefined;
    shininess: number | undefined;
    shaderType: DashShaderType | undefined;
    opacity: number | undefined;
}
```

### Fields

#### name

The name of the material as a string. This field is required. The max length of the string is **31** characters to conform with the binary version of the file format. The name is required as editing programs require materials to have a name.

In cases for exporting a material with no name to the `.dmx` format, the default behavior will be to assign the material a name in the format of `material-%03d` with the index of the material being zero padded three characters.

Reference: [https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.name](https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.name)

#### transparent

A boolean to value to indicate if the material uses alpha or not. The determines if the material uses the alpha channel for the diffuse color (`.color`), diffuse texture(`.map`) and vertex colors. The `opacity` value will be ignored if this value is `false`.

Default is `false`.

Reference: [https://threejs.org/docs/index.html#api/en/materials/Material.transparent](https://threejs.org/docs/index.html#api/en/materials/Material.transparent)

#### alphaTest

Sets the alpha value to be used when running an alpha test. The material will not be rendered if the opacity is lower than this value.

Default is `0`.

Reference: [https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.alphaTest](https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.alphaTest)

#### visible

Defines whether this material is visible.

Default is `true`.

Reference: [https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.visible](https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.visible)

#### color

The diffuse color for the material. 

Expected format an color value in the functional notation is ‘rgb(’ followed by a comma-separated list of three numerical values, three integer values between 0 and 255 corresponding to red, green, and blue values followed by ‘)’.

Default is: `rgb(255, 255, 255)`

Reference: [https://threejs.org/docs/index.html?q=mater#api/en/materials/MeshBasicMaterial.color](https://threejs.org/docs/index.html?q=mater#api/en/materials/MeshBasicMaterial.color)

#### map

The color map. May optionally include an alpha channel, typically combined with `transparent` or `alphaTest`.

Default is `null`.

Reference: [https://threejs.org/docs/index.html#api/en/materials/MeshBasicMaterial.map](https://threejs.org/docs/index.html#api/en/materials/MeshBasicMaterial.map)

#### renderSide

Defines which side of faces will be rendered - front, back or both. Default is `DashMaterialSide.FrontSide`. Other options are `DashMaterialSide.BackSide` and `DashMaterialSide.DoubleSide`.

If `null`, the side casting shadows is determined as follows:

| Material.renderSide         | Side casting shadows |
| --------------------------- | -------------------- |
| DashMaterialSide.FrontSide  | back side            |
| DashMaterialSide.BackSide   | front side           |
| DashMaterialSide.DoubleSide | both sides           |

Default is: `DashMaterialSide.FrontSide`

Reference: [https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.side](https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.side)

#### vertexColors

Defines whether vertex coloring is used.

Default is `false`.

Reference: [https://threejs.org/docs/index.html#api/en/materials/Material.vertexColors](https://threejs.org/docs/index.html#api/en/materials/Material.vertexColors)

#### blending

Which blending to use when displaying objects with this material.
This must be set to CustomBlending to use custom blendSrc, blendDst or blendEquation.
See the blending mode constants for all possible values. 

Default is `normal`. 

Reference: https://threejs.org/docs/#api/en/materials/Material.blending

#### blendEquation

Blending equation to use when applying blending. See the blending equation constants for all possible values.

The material's blending must be set to CustomBlending for this to have any effect. 

Default is `add`.

Reference: https://threejs.org/docs/#api/en/materials/Material.blendEquation

#### blendSrc

Blending source. See the source factors constants for all possible values.
The material's blending must be set to CustomBlending for this to have any effect. 

Default is `SrcAlphaFactor`.

Reference: https://threejs.org/docs/#api/en/materials/Material.blendSrc

#### blendDst

Blending destination. See the destination factors constants for all possible values.
The material's blending must be set to CustomBlending for this to have any effect. 

Default is `OneMinusSrcAlphaFactor`.

Reference: https://threejs.org/docs/#api/en/materials/Material.blendDst

#### emissive

Emissive (light) color of the material, essentially a solid color unaffected by other lighting. The material's shader must be set to `phong` for this to have any effect.

Expected format an color value in the functional notation is ‘rgb(’ followed by a comma-separated list of three numerical values, three integer values between 0 and 255 corresponding to red, green, and blue values followed by ‘)’.

Default is: `rgb(0, 0, 0)`

Reference: https://threejs.org/docs/#api/en/materials/MeshPhongMaterial.emissive

#### emissiveIntensity

Intensity of the emissive light. Modulates the emissive color. The material's shader must be set to `phong` for this to have any effect.

Default is `1`.

https://threejs.org/docs/#api/en/materials/MeshPhongMaterial.emissiveIntensity

#### specular

Specular color of the material. The material's shader must be set to `phong` or `lambert` for this to have any effect.

Default is: `rgb(17, 17, 17)`

Reference: https://threejs.org/docs/#api/en/materials/MeshPhongMaterial.specular

#### shininess

How shiny the .specular highlight is; a higher value gives a sharper highlight.

Default is `30`.

https://threejs.org/docs/#api/en/materials/MeshPhongMaterial.shininess

#### shaderType

Indicates the shader type for the material. Options are `basic`, `lambert` and `phong`. 

#### opacity

Float in the range of 0.0 - 1.0 indicating how transparent the material is. A value of 0.0 indicates fully transparent, 1.0 is fully opaque.

If the material's transparent property is not set to `true`, the material will remain fully opaque and this value will only affect its color.

Default is `1`. 

Reference: https://threejs.org/docs/#api/en/materials/Material.opacity


#### Enums

```typescript
enum DashShaderType {
  Basic = "basic",
  Lambert = "lambert",
  Phong = "phong",
}

enum DashMaterialSide {
  FrontSide = "front",
  BackSide = "back",
  DoubleSide = "double",
}

enum DashBlending {
  NoBlending = "none",  
  NormalBlending = "normal", 
  AdditiveBlending = "additive", 
  SubtractiveBlending = "subtractive", 
  MultiplyBlending = "multiply",  
  CustomBlending = "custom", 
}

enum DashBlendingEquations {
  AddEquation = "add", 
  SubtractEquation = "subtract", 
  ReverseSubtractEquation = "reverseSubtract", 
  MinEquation = "min",
  MaxEquation = "max",
}

enum DashSourceFactors {
  ZeroFactor = "zero",
  OneFactor = "one",
  SrcColorFactor = "srcColor",
  OneMinusSrcColorFactor = "oneMinusSrcColor",
  SrcAlphaFactor = "srcAplha",
  OneMinusSrcAlphaFactor = "oneMinusSrcAlpha",
  DstAlphaFactor = "dstAlpha",
  OneMinusDstAlphaFactor = "oneMinusDstAlpha",
  DstColorFactor = "dstColor",
  OneMinusDstColorFactor = "oneMinusDstColor",
  SrcAlphaSaturateFactor = "srcAlphaSaturate",
}
```

## Binary

### Struct

```c
typedef struct {
	char name[0x20];
	uint32_t index;
	uint32_t visible;
  uint32_t transparent;
  uint32_t useVertexColor;
  uint32_t renderSide;
  float alphaTest;
  uint32_t useMap;
  uint32_t mapIndex;
  uint32_t shader;
  uint8_t color[4];
  uint8_t emissive[4];
  uint8_t specular[4];
  uint32_t blending;
  uint32_t blendingEquation; 
  uint32_t blendingSrc;
  uint32_t blendingDst;

} DashMaterial;
```

### Table

| Offset | 0x00          | 0x04             | 0x08          | 0x0c          |
| ------ | ------------- | ---------------- | ------------- | ------------- |
| 0x0000 | name | 0000             | 0000          | 0000          |
| 0x0010 | 0000          | 0000             | 0000          | 0000          |
| 0x0020 | index         |  visible         | transparent   | useVertexColor |
| 0x0030 | renderSide    | alphaTest        | useMap        | mapIndex      |
| 0x0040 | shader    |             |  |  |
| 0x0050 | blending      | blendingEquation | blendingSrc   | blendingDst   |
| 0x0060 | diffuse[0] | diffuse[1] | diffuse[2] | transparency |
| 0x0070 | specular[0] | specular[1] | specular[2] | shininess |
| 0x0080 | emissive[0] | emissive[1] | emissive[2] | emissiveIntensity |


### Terms

The binary format of the material format uses the same 

### **Constants**

```c
// Shader Types

#define DASH_MATERIAL_BASIC               0
#define DASH_MATERIAL_LAMBERT             1
#define DASH_MATERIAL_PHONG               2

// Render Side

enum DashMaterialSide {
  FrontSide = 0,
  BackSide = 1,
  DoubleSide = 2,
}

#define DASH_MATERIAL_FRONTSIDE           0
#define DASH_MATERIAL_BACKSIDE            1
#define DASH_MATERIAL_DOUBLESIDE          2

// Blending

enum DashBlending {
  NoBlending = 0,  
  NormalBlending = 1, 
  AdditiveBlending = 2, 
  SubtractiveBlending = 3, 
  MultiplyBlending = 4,  
  CustomBlending = 5, 
}

// Blend Equations

enum DashBlendingEquations {
  AddEquation = 100, 
  SubtractEquation = 101, 
  ReverseSubtractEquation = 102, 
  MinEquation = 103,
  MaxEquation = 104,
}

#define DASH_MATERIAL_NORMAL              0
#define DASH_MATERIAL_ADDITIVE            1
#define DASH_MATERIAL_SUBTRACT            2
#define DASH_MATERIAL_MULTIPLY            3

// Blend Contansts

enum DashSourceFactors {
  ZeroFactor = 200,
  OneFactor = 201,
  SrcColorFactor = 202,
  OneMinusSrcColorFactor = 203,
  SrcAlphaFactor = 204,
  OneMinusSrcAlphaFactor = 205,
  DstAlphaFactor = 206,
  OneMinusDstAlphaFactor = 207,
  DstColorFactor = 208,
  OneMinusDstColorFactor = 209,
  SrcAlphaSaturateFactor = 210,
}

#define DASH_MATERIAL_ZERO                0
#define DASH_MATERIAL_ONE                 1
#define DASH_MATERIAL_SRC_COLOR           2
#define DASH_MATERIAL_ONE_MINUS_SRC_COLOR 3
#define DASH_MATERIAL_SRC_ALPHA           4
#define DASH_MATERIAL_ONE_MINUS_SRC_ALPHA 5
#define DASH_MATERIAL_DST_ALPHA           6
#define DASH_MATERIAL_ONE_MINUS_DST_ALPHA 7
#define DASH_MATERIAL_DST_COLOR           8
#define DASH_MATERIAL_ONE_MINUS_DST_COLOR 9
#define DASH_MATERIAL_SRC_ALPHA_SATURATE  10
```
