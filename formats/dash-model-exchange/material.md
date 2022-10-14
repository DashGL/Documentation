---
description: Structures and linked data definitions for materials
---

# Material

## Json

The only required field for `Materials` is the `name`. All other fields will provide default values if not provided.&#x20;

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
	"shadowSide": "front",
	"vertexColor" : true
	"blending" : "custom",
	"blendEquation" : "additive",
	"blendSrc" : "srcAlphaFactor",
	"blendDst" : "oneMinusSrcAlphaFactor",
	"emissiveColor": "#rgb(0,0,0)",
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
    specularColor: string | undefined;
    shininess: number | undefined;
    shaderType: DashShaderType | undefined;
    opacity: number | undefined;
}
```

### Fields

#### name

The name of the material as a string. This field is required. The max length of the string is **31** characters to conform with the binary version of the file format. The name is required as editing programs require materials to have a name.&#x20;

In cases for exporting a material with no name to the `.dmx` format, the default behavior will be to assign the material a name in the format of `material-%03d` with the index of the material being zero padded three characters.&#x20;

Reference: [https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.name](https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.name)

#### transparent

A boolean to value to indicate if the material uses alpha or not. The determines if the material uses the alpha channel for the diffuse color (`.color`), diffuse texture(`.map`) and vertex colors. The `opacity` value will be ignored if this value is `false`.&#x20;

Default is `false`.

Reference: [https://threejs.org/docs/index.html#api/en/materials/Material.transparent](https://threejs.org/docs/index.html#api/en/materials/Material.transparent)

#### alphaTest

Sets the alpha value to be used when running an alpha test. The material will not be rendered if the opacity is lower than this value.&#x20;

Default is `0`.

Reference: [https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.alphaTest](https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.alphaTest)

#### visible

Defines whether this material is visible.&#x20;

Default is `true`.

Reference: [https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.visible](https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.visible)

#### color

The diffuse color for the material. Expected format an color value in the functional notation is ‘rgb(’ followed by a comma-separated list of three numerical values, three integer values between 0 and 255 corresponding to red, green, and blue values followed by ‘)’.

Default is: `rgb(255, 255, 255)`

Reference: [https://threejs.org/docs/index.html?q=mater#api/en/materials/MeshBasicMaterial.color](https://threejs.org/docs/index.html?q=mater#api/en/materials/MeshBasicMaterial.color)

#### map

The color map. May optionally include an alpha channel, typically combined with `transparent` or `alphaTest`.&#x20;

Default is `null`.

Reference: [https://threejs.org/docs/index.html#api/en/materials/MeshBasicMaterial.map](https://threejs.org/docs/index.html#api/en/materials/MeshBasicMaterial.map)

#### renderSide

Defines which side of faces will be rendered - front, back or both. Default is `DashMaterialSide.FrontSide`. Other options are `DashMaterialSide.BackSide` and `DashMaterialSide.DoubleSide`.

Default is: `DashMaterialSide.FrontSide`

Reference: [https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.side](https://threejs.org/docs/index.html?q=mater#api/en/materials/Material.side)

#### shadowSide

Defines which side of faces cast shadows. When set, can be `DashMaterialSide.FrontSide`, `DashMaterialSide.BackSide`, or `DashMaterialSide.DoubleSide`.&#x20;

Default is `null`.

If `null`, the side casting shadows is determined as follows:

| Material.renderSide         | Side casting shadows |
| --------------------------- | -------------------- |
| DashMaterialSide.FrontSide  | back side            |
| DashMaterialSide.BackSide   | front side           |
| DashMaterialSide.DoubleSide | both sides           |

Reference: [https://threejs.org/docs/index.html#api/en/materials/Material.shadowSide](https://threejs.org/docs/index.html#api/en/materials/Material.shadowSide)

#### vertexColors

Defines whether vertex coloring is used.&#x20;

Default is `false`.

Reference: [https://threejs.org/docs/index.html#api/en/materials/Material.vertexColors](https://threejs.org/docs/index.html#api/en/materials/Material.vertexColors)

### Enums

<pre class="language-typescript"><code class="lang-typescript">enum DashShaderType {
  Basic = "basic",
  Lambert = "lambert",
  Phong = "phong",
}

<strong>enum DashMaterialSide {
</strong>  FrontSide = "front",
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
}</code></pre>

## Binary

### Struct

```c
typedef struct {
	char name[0x20];
	int16_t mat_id;
	int16_t tex_id;
	uint16_t use_blending;
	uint16_t blend_equation;
	uint16_t blend_src;
	uint16_t blend_dst;
	uint16_t skinning;
	uint16_t shader_type;
	uint16_t face_side;
	uint16_t shadow_side;
	uint16_t ignore_lights;
	uint16_t vertex_color;
	uint16_t use_alpha;
	uint16_t skip_render;
	float alpha_test;
	float diffuse[4];
	float emissive[4];
	float specular[4];
} DashMaterial;
```

### Table

| Offset | 0x00          | 0x04             | 0x08          | 0x0c          |
| ------ | ------------- | ---------------- | ------------- | ------------- |
| 0x0000 | Material Name | 0000             | 0000          | 0000          |
| 0x0010 | 0000          | 0000             | 0000          | 0000          |
| 0x0020 | index         | transparent      |               | alphaTest     |
| 0x0030 |               | useVertexColor   |               | visible       |
| 0x0040 | renderSide    | shadowSide       | useMap        | mapIndex      |
| 0x0050 | shaderType    | color            | emissiveColor | specularColor |
| 0x0060 | blending      | blendingEquation | blendingSrc   | blendingDst   |

### Terms

The Dash Model format material definition is based around the Phong shader type, which includes diffuse, emissive and specular definitions. If all of these attributes are not required, the shader\_type paramter can be set to basic or lambert, in which case all of the attributes for phong will still be present in the file (using default values), but the loader will ignore them onload.

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
