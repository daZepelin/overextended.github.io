# Points

Simple and centralised distance checking, supporting callbacks when entering, leaving, and standing in-range of set coordinates.

### CPoint

A table representing a point, with the following properties.

* id: `number`
* coords: `vector3`
* distance: `number`
  * The distance for the player to be "inside" a point (i.e. the point's radius).
* currentDistance: `number`
  * The players current distance from the centre of the point.
* isClosest?: `boolean`
* remove: `function()`
  * Removes the point from the points registry.

### lib.points.new

```lua
lib.points.new(data)
```

* data: `table`
  * coords: `vector3`
  * distance: `number`

**Returns:** CPoint

```lua
local point = lib.points.new({
    coords = GetEntityCoords(cache.ped),
    distance = 5,
    dunak = 'nerd',
})

function point:onEnter()
    print('entered range of point', self.id)
end

function point:onExit()
    print('left range of point', self.id)
end

function point:nearby()
    DrawMarker(2, self.coords.x, self.coords.y, self.coords.z, 0.0, 0.0, 0.0, 0.0, 180.0, 0.0, 1.0, 1.0, 1.0, 200, 20, 20, 50, false, true, 2, nil, nil, false)

    if self.currentDistance < 1 and IsControlJustReleased(0, 38) then
        print('inside marker', self.id, 'dunak is a '.. self.dunak)
    end
end
```

### lib.points.getAllPoints

Get a table of all points created in the resource.

```lua
lib.points.getAllPoints()
```

**Return:** `table<number, CPoint>`

### lib.points.getNearbyPoints

Get an array of all points in range of the player.

```lua
lib.points.getNearbyPoints()
```

**Return:** `CPoint[]`

### lib.points.getClosestPoint

Get the data for the closest point to the player.

```lua
lib.points.getClosestPoint()
```

**Returns:** `CPoint`
