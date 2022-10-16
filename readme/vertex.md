# Vertex

## JSON

### Format

```json
{
	"x": 0,
	"y": 0,
	"z": 0,
	"influence": [{
		"index": 0,
		"weight": 0
	}]
}
```

### Type

```typescript
type Dashinfluence = {
	index: number;
	weight: number;
}

type DashVertex = {
	x: number,
	y: number,
	z: number,
	influence: Dashinfluence[] | undefined;
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





## Binary
