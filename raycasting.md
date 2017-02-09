# Casting Rays

In order to build a raytracer, you must cast rays through each pixel on the screen, and determine if it collides with an object or not.

```swift
public func castRay(ray: Ray,
                    bounceDepth: Int,
                    objects: [Intersectable]) -> Color {
```
