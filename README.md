# Auios.QuadTree
A Generic QuadTree algorithm inspired by [Leonidovia's Ultimate QuadTree.](https://github.com/leonidovia/UltimateQuadTree)

Wikipedia - https://en.wikipedia.org/wiki/Quadtree

## Example

```cs
// Implement IQuadTreeObjectBounds<T> interface for the object type to be stored
public class MyCustomBounds : IQuadTreeObjectBounds<Vector2>
{
    public float GetLeft(Vecto2 obj)
    {
        return obj.Min(p => p.X);
    }

    public float GetRight(Vector2 obj)
    {
        return obj.Max(p => p.X);
    }

    public float GetTop(Vector2 obj)
    {
        return obj.Min(p => p.Y);
    }

    public float GetBottom(Vector2 obj)
    {
        return obj.Max(p => p.Y);
    }
}

// Create a QuadTree and fill it with objects
QuadTree<Vector2> quadTree = new QuadTree<Vector2>(800, 600, new MyCustomBounds());

// Generate some data to insert
Random random = new Random();
List<Vector2> myPositions = new List<Vector2>();
for(int i = 0; i < 1000; i++)
{
    myPositions.Add(new Vector2((float)800 * random.NextDouble(), (float)600 * random.NextDouble()));
}

 // Insert data into the QuadTree
foreach(Vector2 position in myPositions)
{
    quadTree.Insert(myObjects);
}

// Define search area (x, y, width, height)
QuadTreeRect searchArea = new QuadTreeRect(150, 100, 50, 25);

// Find objects in leaf quadrants which overlap the search area
Vector2[] positions = quadTree.FindObjects(searchArea);
```