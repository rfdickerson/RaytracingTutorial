# Spheres

I will create a simple sphere first. 

```swift
public struct Sphere {
   public let radius: Double
}
```

The intersection of a ray with a sphere can be solved by determining the roots of a quadratic. 

$$a^2 + b^2 = c^2$$


```swift
public func intersect(ray: Ray) -> Collision? {
        
        // transform ray to object space
        let center = objectToWorld * Vector3D(0, 0, 0)
    
        let L = ray.origin - center
        
        let a = dot(ray.direction, ray.direction)
        let b = 2 * dot(ray.direction, L)
        let c = dot(L, L) - radiusSquared
        
        guard let roots = solveQuadratic(a: a, b: b, c: c) else {
            return nil
        }
        
        let t0 = min(roots.0, roots.1)
        let t1 = max(roots.0, roots.1)
        
        if t0<0 && t1<0 {
            return nil
        }
        
        let intersection = ray.origin + t0 * ray.direction
        
        // let center = objectToWorld * Vector3D(0,0,0)
        
        let normal = norm(center - intersection)
        
        return Collision(intersection: intersection, normal: normal, tangent: nil, bitangent: nil, depth: t0)
        
    }
```
