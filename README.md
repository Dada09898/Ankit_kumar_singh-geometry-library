# Ankit_kumar_singh-geometry-library
#he fundamental geometric shapes, their properties, and the basic operations to be included in the library, and note the scope.
# 1. Essential 2D geometric shapes
shapes = ["Point", "Line", "Circle", "Rectangle", "Polygon"]

# 2. Fundamental properties of each shape
shape_properties = {
    "Point": ["x_coordinate", "y_coordinate"],
    "Line": ["point1", "point2"], # A line can be defined by two points
    "Circle": ["center_point", "radius"],
    "Rectangle": ["top_left_point", "width", "height"], # Or by two opposite points
    "Polygon": ["list_of_points"]
}

# 3. Basic operations on these shapes
basic_operations = [
    "distance_between_points",
    "length_of_line",
    "area_of_circle",
    "perimeter_of_circle",
    "area_of_rectangle",
    "perimeter_of_rectangle",
    "area_of_polygon",
    "perimeter_of_polygon",
    "intersection_of_lines",
    "point_on_line",
    "point_in_circle",
    "point_in_rectangle",
    "point_in_polygon"
]

# 4. Scope of the library
scope = "Focus on 2D geometry for now, with potential for 3D geometry in the future."

print("Essential 2D Geometric Shapes:", shapes)
print("\nFundamental Properties:")
for shape, properties in shape_properties.items():
    print(f"- {shape}: {', '.join(properties)}")

print("\nBasic Operations:", basic_operations)
print("\nScope:", scope)


#Create the Python classes for Point, Line, Circle, Rectangle, and Polygon as specified in the instructions to represent the geometric concepts.
class Point:
    """Represents a point in 2D space."""
    def __init__(self, x_coordinate, y_coordinate):
        self.x_coordinate = x_coordinate
        self.y_coordinate = y_coordinate

    def __repr__(self):
        return f"Point(x={self.x_coordinate}, y={self.y_coordinate})"

class Line:
    """Represents a line defined by two points."""
    def __init__(self, point1, point2):
        if not isinstance(point1, Point) or not isinstance(point2, Point):
            raise TypeError("Both point1 and point2 must be Point objects.")
        self.point1 = point1
        self.point2 = point2

    def __repr__(self):
        return f"Line(point1={self.point1}, point2={self.point2})"

class Circle:
    """Represents a circle."""
    def __init__(self, center_point, radius):
        if not isinstance(center_point, Point):
            raise TypeError("center_point must be a Point object.")
        if not isinstance(radius, (int, float)) or radius < 0:
            raise ValueError("radius must be a non-negative number.")
        self.center_point = center_point
        self.radius = radius

    def __repr__(self):
        return f"Circle(center={self.center_point}, radius={self.radius})"

class Rectangle:
    """Represents a rectangle."""
    def __init__(self, top_left_point, width, height):
        if not isinstance(top_left_point, Point):
            raise TypeError("top_left_point must be a Point object.")
        if not isinstance(width, (int, float)) or width < 0:
            raise ValueError("width must be a non-negative number.")
        if not isinstance(height, (int, float)) or height < 0:
            raise ValueError("height must be a non-negative number.")
        self.top_left_point = top_left_point
        self.width = width
        self.height = height

    def __repr__(self):
        return f"Rectangle(top_left={self.top_left_point}, width={self.width}, height={self.height})"

class Polygon:
    """Represents a polygon."""
    def __init__(self, list_of_points):
        if not isinstance(list_of_points, list) or not all(isinstance(p, Point) for p in list_of_points):
            raise TypeError("list_of_points must be a list of Point objects.")
        if len(list_of_points) < 3:
             raise ValueError("A polygon must have at least 3 points.")
        self.list_of_points = list_of_points

    def __repr__(self):
        return f"Polygon(points={self.list_of_points})"

# Example Usage (Optional, for verification)
p1 = Point(0, 0)
p2 = Point(1, 1)
line = Line(p1, p2)
circle = Circle(p1, 5)
rectangle = Rectangle(p1, 10, 5)
polygon = Polygon([Point(0,0), Point(1,0), Point(1,1), Point(0,1)])

print(p1)
print(line)
print(circle)
print(rectangle)
print(polygon)


import math

def distance(point1, point2):
    """Calculates the distance between two Point objects."""
    if not isinstance(point1, Point) or not isinstance(point2, Point):
        raise TypeError("Both inputs must be Point objects.")
    return math.sqrt((point2.x_coordinate - point1.x_coordinate)**2 + (point2.y_coordinate - point1.y_coordinate)**2)

def line_length(line):
    """Calculates the length of a Line object."""
    if not isinstance(line, Line):
        raise TypeError("Input must be a Line object.")
    return distance(line.point1, line.point2)

def circle_area(circle):
    """Calculates the area of a Circle object."""
    if not isinstance(circle, Circle):
        raise TypeError("Input must be a Circle object.")
    return math.pi * circle.radius**2

def circle_perimeter(circle):
    """Calculates the perimeter (circumference) of a Circle object."""
    if not isinstance(circle, Circle):
        raise TypeError("Input must be a Circle object.")
    return 2 * math.pi * circle.radius

def rectangle_area(rectangle):
    """Calculates the area of a Rectangle object."""
    if not isinstance(rectangle, Rectangle):
        raise TypeError("Input must be a Rectangle object.")
    return rectangle.width * rectangle.height

def rectangle_perimeter(rectangle):
    """Calculates the perimeter of a Rectangle object."""
    if not isinstance(rectangle, Rectangle):
        raise TypeError("Input must be a Rectangle object.")
    return 2 * (rectangle.width + rectangle.height)

def polygon_area(polygon):
    """Calculates the area of a Polygon object using the shoelace formula."""
    if not isinstance(polygon, Polygon):
        raise TypeError("Input must be a Polygon object.")
    points = polygon.list_of_points
    n = len(points)
    area = 0.0
    for i in range(n):
        j = (i + 1) % n
        area += points[i].x_coordinate * points[j].y_coordinate
        area -= points[j].x_coordinate * points[i].y_coordinate
    area = abs(area) / 2.0
    return area

def polygon_perimeter(polygon):
    """Calculates the perimeter of a Polygon object."""
    if not isinstance(polygon, Polygon):
        raise TypeError("Input must be a Polygon object.")
    points = polygon.list_of_points
    n = len(points)
    perimeter = 0.0
    for i in range(n):
        j = (i + 1) % n
        perimeter += distance(points[i], points[j])
    return perimeter

# Example Usage
p1 = Point(0, 0)
p2 = Point(3, 4)
line = Line(p1, p2)
circle = Circle(p1, 5)
rectangle = Rectangle(p1, 10, 5)
polygon = Polygon([Point(0,0), Point(4,0), Point(4,3), Point(0,3)]) # A square of side 4

print(f"Distance between {p1} and {p2}: {distance(p1, p2)}")
print(f"Length of {line}: {line_length(line)}")
print(f"Area of {circle}: {circle_area(circle)}")
print(f"Perimeter of {circle}: {circle_perimeter(circle)}")
print(f"Area of {rectangle}: {rectangle_area(rectangle)}")
print(f"Perimeter of {rectangle}: {rectangle_perimeter(rectangle)}")
print(f"Area of {polygon}: {polygon_area(polygon)}")
print(f"Perimeter of {polygon}: {polygon_perimeter(polygon)}")



#Add comprehensive docstrings with examples to the existing classes and functions.


import math

class Point:
    """
    Represents a point in 2D space.

    Attributes:
        x_coordinate (float): The x-coordinate of the point.
        y_coordinate (float): The y-coordinate of the point.

    Examples:
        >>> p = Point(5, 10)
        >>> p.x_coordinate
        5
        >>> p.y_coordinate
        10
    """
    def __init__(self, x_coordinate, y_coordinate):
        self.x_coordinate = x_coordinate
        self.y_coordinate = y_coordinate

    def __repr__(self):
        return f"Point(x={self.x_coordinate}, y={self.y_coordinate})"

class Line:
    """
    Represents a line defined by two Point objects.

    Attributes:
        point1 (Point): The first Point object defining the line.
        point2 (Point): The second Point object defining the line.

    Raises:
        TypeError: If point1 or point2 are not Point objects.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(3, 4)
        >>> line = Line(p1, p2)
        >>> line.point1
        Point(x=0, y=0)
        >>> line.point2
        Point(x=3, y=4)
    """
    def __init__(self, point1, point2):
        if not isinstance(point1, Point) or not isinstance(point2, Point):
            raise TypeError("Both point1 and point2 must be Point objects.")
        self.point1 = point1
        self.point2 = point2

    def __repr__(self):
        return f"Line(point1={self.point1}, point2={self.point2})"

class Circle:
    """
    Represents a circle.

    Attributes:
        center_point (Point): The center Point object of the circle.
        radius (float): The radius of the circle.

    Raises:
        TypeError: If center_point is not a Point object.
        ValueError: If radius is not a non-negative number.

    Examples:
        >>> center = Point(0, 0)
        >>> circle = Circle(center, 5)
        >>> circle.center_point
        Point(x=0, y=0)
        >>> circle.radius
        5
        >>> Circle(center, -2)
        Traceback (most recent call last):
            ...
        ValueError: radius must be a non-negative number.
    """
    def __init__(self, center_point, radius):
        if not isinstance(center_point, Point):
            raise TypeError("center_point must be a Point object.")
        if not isinstance(radius, (int, float)) or radius < 0:
            raise ValueError("radius must be a non-negative number.")
        self.center_point = center_point
        self.radius = radius

    def __repr__(self):
        return f"Circle(center={self.center_point}, radius={self.radius})"

class Rectangle:
    """
    Represents a rectangle defined by its top-left corner, width, and height.

    Attributes:
        top_left_point (Point): The top-left Point object of the rectangle.
        width (float): The width of the rectangle.
        height (float): The height of the rectangle.

    Raises:
        TypeError: If top_left_point is not a Point object.
        ValueError: If width or height are not non-negative numbers.

    Examples:
        >>> top_left = Point(1, 5)
        >>> rectangle = Rectangle(top_left, 10, 5)
        >>> rectangle.top_left_point
        Point(x=1, y=5)
        >>> rectangle.width
        10
        >>> rectangle.height
        5
    """
    def __init__(self, top_left_point, width, height):
        if not isinstance(top_left_point, Point):
            raise TypeError("top_left_point must be a Point object.")
        if not isinstance(width, (int, float)) or width < 0:
            raise ValueError("width must be a non-negative number.")
        if not isinstance(height, (int, float)) or height < 0:
            raise ValueError("height must be a non-negative number.")
        self.top_left_point = top_left_point
        self.width = width
        self.height = height

    def __repr__(self):
        return f"Rectangle(top_left={self.top_left_point}, width={self.width}, height={self.height})"

class Polygon:
    """
    Represents a polygon defined by a list of Point objects.

    The points should be listed in order, either clockwise or counter-clockwise.

    Attributes:
        list_of_points (list[Point]): A list of Point objects defining the vertices of the polygon.

    Raises:
        TypeError: If list_of_points is not a list or contains non-Point objects.
        ValueError: If the number of points is less than 3.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(4, 0)
        >>> p3 = Point(4, 3)
        >>> p4 = Point(0, 3)
        >>> polygon = Polygon([p1, p2, p3, p4])
        >>> polygon.list_of_points
        [Point(x=0, y=0), Point(x=4, y=0), Point(x=4, y=3), Point(x=0, y=3)]
        >>> Polygon([p1, p2])
        Traceback (most recent call last):
            ...
        ValueError: A polygon must have at least 3 points.
    """
    def __init__(self, list_of_points):
        if not isinstance(list_of_points, list) or not all(isinstance(p, Point) for p in list_of_points):
            raise TypeError("list_of_points must be a list of Point objects.")
        if len(list_of_points) < 3:
             raise ValueError("A polygon must have at least 3 points.")
        self.list_of_points = list_of_points

    def __repr__(self):
        return f"Polygon(points={self.list_of_points})"

def distance(point1, point2):
    """
    Calculates the Euclidean distance between two Point objects.

    Args:
        point1 (Point): The first Point object.
        point2 (Point): The second Point object.

    Returns:
        float: The distance between the two points.

    Raises:
        TypeError: If point1 or point2 are not Point objects.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(3, 4)
        >>> distance(p1, p2)
        5.0
    """
    if not isinstance(point1, Point) or not isinstance(point2, Point):
        raise TypeError("Both inputs must be Point objects.")
    return math.sqrt((point2.x_coordinate - point1.x_coordinate)**2 + (point2.y_coordinate - point1.y_coordinate)**2)

def line_length(line):
    """
    Calculates the length of a Line object.

    Args:
        line (Line): The Line object.

    Returns:
        float: The length of the line.

    Raises:
        TypeError: If the input is not a Line object.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(3, 4)
        >>> line = Line(p1, p2)
        >>> line_length(line)
        5.0
    """
    if not isinstance(line, Line):
        raise TypeError("Input must be a Line object.")
    return distance(line.point1, line.point2)

def circle_area(circle):
    """
    Calculates the area of a Circle object.

    Args:
        circle (Circle): The Circle object.

    Returns:
        float: The area of the circle.

    Raises:
        TypeError: If the input is not a Circle object.

    Examples:
        >>> center = Point(0, 0)
        >>> circle = Circle(center, 5)
        >>> round(circle_area(circle), 2)
        78.54
    """
    if not isinstance(circle, Circle):
        raise TypeError("Input must be a Circle object.")
    return math.pi * circle.radius**2

def circle_perimeter(circle):
    """
    Calculates the perimeter (circumference) of a Circle object.

    Args:
        circle (Circle): The Circle object.

    Returns:
        float: The perimeter of the circle.

    Raises:
        TypeError: If the input is not a Circle object.

    Examples:
        >>> center = Point(0, 0)
        >>> circle = Circle(center, 5)
        >>> round(circle_perimeter(circle), 2)
        31.42
    """
    if not isinstance(circle, Circle):
        raise TypeError("Input must be a Circle object.")
    return 2 * math.pi * circle.radius

def rectangle_area(rectangle):
    """
    Calculates the area of a Rectangle object.

    Args:
        rectangle (Rectangle): The Rectangle object.

    Returns:
        float: The area of the rectangle.

    Raises:
        TypeError: If the input is not a Rectangle object.

    Examples:
        >>> top_left = Point(1, 5)
        >>> rectangle = Rectangle(top_left, 10, 5)
        >>> rectangle_area(rectangle)
        50
    """
    if not isinstance(rectangle, Rectangle):
        raise TypeError("Input must be a Rectangle object.")
    return rectangle.width * rectangle.height

def rectangle_perimeter(rectangle):
    """
    Calculates the perimeter of a Rectangle object.

    Args:
        rectangle (Rectangle): The Rectangle object.

    Returns:
        float: The perimeter of the rectangle.

    Raises:
        TypeError: If the input is not a Rectangle object.

    Examples:
        >>> top_left = Point(1, 5)
        >>> rectangle = Rectangle(top_left, 10, 5)
        >>> rectangle_perimeter(rectangle)
        30
    """
    if not isinstance(rectangle, Rectangle):
        raise TypeError("Input must be a Rectangle object.")
    return 2 * (rectangle.width + rectangle.height)

def polygon_area(polygon):
    """
    Calculates the area of a Polygon object using the shoelace formula.

    Args:
        polygon (Polygon): The Polygon object.

    Returns:
        float: The area of the polygon.

    Raises:
        TypeError: If the input is not a Polygon object.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(4, 0)
        >>> p3 = Point(4, 3)
        >>> p4 = Point(0, 3)
        >>> square = Polygon([p1, p2, p3, p4])
        >>> polygon_area(square)
        12.0
    """
    if not isinstance(polygon, Polygon):
        raise TypeError("Input must be a Polygon object.")
    points = polygon.list_of_points
    n = len(points)
    area = 0.0
    for i in range(n):
        j = (i + 1) % n
        area += points[i].x_coordinate * points[j].y_coordinate
        area -= points[j].x_coordinate * points[i].y_coordinate
    area = abs(area) / 2.0
    return area

def polygon_perimeter(polygon):
    """
    Calculates the perimeter of a Polygon object by summing the lengths of its sides.

    Args:
        polygon (Polygon): The Polygon object.

    Returns:
        float: The perimeter of the polygon.

    Raises:
        TypeError: If the input is not a Polygon object.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(4, 0)
        >>> p3 = Point(4, 3)
        >>> p4 = Point(0, 3)
        >>> square = Polygon([p1, p2, p3, p4])
        >>> polygon_perimeter(square)
        14.0
        >>> triangle = Polygon([Point(0,0), Point(3,0), Point(0,4)])
        >>> polygon_perimeter(triangle)
        12.0
    """
    if not isinstance(polygon, Polygon):
        raise TypeError("Input must be a Polygon object.")
    points = polygon.list_of_points
    n = len(points)
    perimeter = 0.0
    for i in range(n):
        j = (i + 1) % n
        perimeter += distance(points[i], points[j])
    return perimeter




#Outline advanced features for the geometry library, considering transformations and 3D geometry, and document their potential implementation approaches within the existing class structure.


# 1. Consider advanced features
advanced_features = {
    "Transformations": ["Translation", "Rotation", "Scaling"],
    "3D Geometry": ["Point (3D)", "Line (3D)", "Sphere", "Cube"],
    "Advanced Operations": ["Intersection of shapes", "Convex Hull", "Closest Point"]
}

# 2. Outline implementation approaches for considered advanced features

# Transformations
# Add methods to existing 2D classes (Point, Line, Circle, Rectangle, Polygon)
# Each method would return a *new* transformed object, maintaining immutability.

# Point Translation:
# A `translate(dx, dy)` method in the Point class would return a new Point object
# with coordinates (self.x_coordinate + dx, self.y_coordinate + dy).

# Point Rotation:
# A `rotate(angle, origin)` method in the Point class would return a new Point object
# rotated around the 'origin' point by 'angle' (in radians or degrees).
# This involves trigonometric calculations (cos, sin).

# Point Scaling:
# A `scale(sx, sy, origin)` method in the Point class would return a new Point object
# scaled relative to the 'origin' point by factors 'sx' and 'sy'.

# Transformations for other shapes (Line, Circle, Rectangle, Polygon) would be implemented
# by applying the corresponding point transformations to their defining points
# (e.g., Line transforms its two points, Circle transforms its center, Polygon transforms its list of points).
# Rectangle transformation might require recalculating the top-left point and dimensions based on the transformed vertices.

# 3D Geometry
# Create new classes for 3D shapes (Point3D, Line3D, Sphere, Cube, etc.).
# Point3D would have x, y, z coordinates.
# Line3D would be defined by two Point3D objects.
# Sphere by a center Point3D and radius.
# Cube by a corner Point3D and side length, or by defining points.
# Basic operations (distance, length, surface area, volume) would be implemented for these 3D classes.
# Distance in 3D would use the 3D distance formula.
# 3D Transformations (translation, rotation, scaling) would also be applicable to 3D shapes,
# requiring 3D transformation matrices for more complex rotations.

# Advanced Operations
# Intersection of shapes: Implement functions that take two shape objects and return
# the intersection point(s) or shape(s) (e.g., line-line intersection, circle-circle intersection).
# Convex Hull: Implement a function that takes a list of points and returns the
# Polygon representing their convex hull. Algorithms like Graham scan or Monotone Chain could be used.
# Closest Point: Implement functions to find the closest point on a shape (e.g., line, circle)
# to a given point.

# 3. Document potential advanced features and their planned implementation approaches.
documentation_advanced_features = """
## Advanced Features

This section outlines potential advanced features that could be added to the geometry library in the future.

### Transformations

Adding transformation capabilities (translation, rotation, scaling) would allow users to manipulate geometric objects.

-   **Translation:** Moving a shape by a certain distance in the x and y (and z for 3D) directions.
    -   *Implementation:* Add a `translate(dx, dy)` method to each 2D shape class (Point, Line, Circle, Rectangle, Polygon). This method would return a *new* shape object with its defining points/properties adjusted by `dx` and `dy`. For Point, it's a simple coordinate addition. For other shapes, it involves translating their constituent points.
-   **Rotation:** Rotating a shape around a specified origin point by a certain angle.
    -   *Implementation:* Add a `rotate(angle, origin)` method to each 2D shape class. This involves applying rotation formulas to the defining points of the shapes relative to the origin. Trigonometric functions (sine and cosine) will be used.
-   **Scaling:** Resizing a shape relative to a specified origin point by scale factors.
    -   *Implementation:* Add a `scale(sx, sy, origin)` method to each 2D shape class. This involves scaling the distances of the defining points from the origin by `sx` and `sy`.

### 3D Geometry

Extending the library to 3D would introduce new shapes and operations.

-   **3D Shapes:**
    -   `Point3D(x, y, z)`: Represents a point in 3D space.
    -   `Line3D(point1, point2)`: Represents a line in 3D defined by two `Point3D` objects.
    -   `Sphere(center_point, radius)`: Represents a sphere defined by a `Point3D` center and radius.
    -   `Cube`, `Cylinder`, etc.
    -   *Implementation:* Create new classes for each 3D shape, similar to the 2D classes, with appropriate attributes (e.g., z-coordinate for `Point3D`).
-   **Basic 3D Operations:**
    -   Distance between `Point3D` objects.
    -   Length of `Line3D`.
    -   Surface area and volume of 3D shapes (Sphere, Cube, etc.).
    -   *Implementation:* Implement functions for these operations using the 3D counterparts of the formulas.
-   **3D Transformations:** Translation, rotation (potentially using rotation matrices for more complex scenarios), and scaling in 3D.
    -   *Implementation:* Add `translate(dx, dy, dz)`, `rotate(...)`, and `scale(sx, sy, sz, origin)` methods to 3D shape classes.

### Advanced Operations

More complex geometric algorithms could be included.

-   **Intersection of Shapes:** Finding the common point(s) or region between two shapes.
    -   *Implementation:* Implement functions like `intersect_lines(line1, line2)`, `intersect_circles(circle1, circle2)`, etc. These would involve solving systems of equations based on the shape definitions.
-   **Convex Hull:** Finding the smallest convex polygon that contains a given set of points.
    -   *Implementation:* Implement a `convex_hull(list_of_points)` function using an algorithm like Graham scan or Monotone Chain.
-   **Closest Point:** Finding the point on a shape that is nearest to a given point.
    -   *Implementation:* Implement functions like `closest_point_on_line(point, line)`, `closest_point_on_circle(point, circle)`. These would involve geometric formulas and potentially optimization techniques.
"""

print("Considered Advanced Features:")
for category, features in advanced_features.items():
    print(f"- {category}: {', '.join(features)}")

print("\nPlanned Implementation Approaches (Documentation Snippet):\n")
print(documentation_advanced_features)



##Import the unittest module and define a test class that inherits from unittest.TestCase. Implement test methods for class initialization, including testing for correct attribute setting and handling of invalid inputs by asserting for expected exceptions.


import unittest

class TestGeometry(unittest.TestCase):
    """Unit tests for the geometry library."""

    def test_point_initialization(self):
        """Test Point class initialization."""
        p = Point(10, 20)
        self.assertEqual(p.x_coordinate, 10)
        self.assertEqual(p.y_coordinate, 20)

    def test_line_initialization(self):
        """Test Line class initialization."""
        p1 = Point(0, 0)
        p2 = Point(1, 1)
        line = Line(p1, p2)
        self.assertEqual(line.point1, p1)
        self.assertEqual(line.point2, p2)

        # Test invalid input
        with self.assertRaises(TypeError):
            Line(p1, 123)
        with self.assertRaises(TypeError):
            Line(456, p2)

    def test_circle_initialization(self):
        """Test Circle class initialization."""
        center = Point(0, 0)
        circle = Circle(center, 5)
        self.assertEqual(circle.center_point, center)
        self.assertEqual(circle.radius, 5)

        # Test invalid input
        with self.assertRaises(TypeError):
            Circle(123, 5)
        with self.assertRaises(ValueError):
            Circle(center, -2)
        with self.assertRaises(TypeError):
            Circle(center, "large")

    def test_rectangle_initialization(self):
        """Test Rectangle class initialization."""
        top_left = Point(1, 5)
        rectangle = Rectangle(top_left, 10, 5)
        self.assertEqual(rectangle.top_left_point, top_left)
        self.assertEqual(rectangle.width, 10)
        self.assertEqual(rectangle.height, 5)

        # Test invalid input
        with self.assertRaises(TypeError):
            Rectangle(123, 10, 5)
        with self.assertRaises(ValueError):
            Rectangle(top_left, -10, 5)
        with self.assertRaises(ValueError):
            Rectangle(top_left, 10, -5)
        with self.assertRaises(TypeError):
            Rectangle(top_left, "wide", 5)
        with self.assertRaises(TypeError):
            Rectangle(top_left, 10, "tall")


    def test_polygon_initialization(self):
        """Test Polygon class initialization."""
        points = [Point(0, 0), Point(1, 0), Point(1, 1)]
        polygon = Polygon(points)
        self.assertEqual(polygon.list_of_points, points)

        # Test invalid input
        with self.assertRaises(TypeError):
            Polygon("not a list")
        with self.assertRaises(TypeError):
            Polygon([Point(0,0), "not a point", Point(1,1)])
        with self.assertRaises(ValueError):
            Polygon([Point(0,0), Point(1,0)]) # Less than 3 points
    ###Add test methods to the TestGeometry class to test the basic operations (distance, area, perimeter) for the defined geometric shapes, using assertAlmostEqual for floating-point comparisons and including edge cases.


lass TestGeometry(unittest.TestCase):
    """Unit tests for the geometry library."""

    def test_point_initialization(self):
        """Test Point class initialization."""
        p = Point(10, 20)
        self.assertEqual(p.x_coordinate, 10)
        self.assertEqual(p.y_coordinate, 20)

    def test_line_initialization(self):
        """Test Line class initialization."""
        p1 = Point(0, 0)
        p2 = Point(1, 1)
        line = Line(p1, p2)
        self.assertEqual(line.point1, p1)
        self.assertEqual(line.point2, p2)

        # Test invalid input
        with self.assertRaises(TypeError):
            Line(p1, 123)
        with self.assertRaises(TypeError):
            Line(456, p2)

    def test_circle_initialization(self):
        """Test Circle class initialization."""
        center = Point(0, 0)
        circle = Circle(center, 5)
        self.assertEqual(circle.center_point, center)
        self.assertEqual(circle.radius, 5)

        # Test invalid input
        with self.assertRaises(TypeError):
            Circle(123, 5)
        with self.assertRaises(ValueError):
            Circle(center, -2)
        with self.assertRaises(TypeError):
            Circle(center, "large")

    def test_rectangle_initialization(self):
        """Test Rectangle class initialization."""
        top_left = Point(1, 5)
        rectangle = Rectangle(top_left, 10, 5)
        self.assertEqual(rectangle.top_left_point, top_left)
        self.assertEqual(rectangle.width, 10)
        self.assertEqual(rectangle.height, 5)

        # Test invalid input
        with self.assertRaises(TypeError):
            Rectangle(123, 10, 5)
        with self.assertRaises(ValueError):
            Rectangle(top_left, -10, 5)
        with self.assertRaises(ValueError):
            Rectangle(top_left, 10, -5)
        with self.assertRaises(TypeError):
            Rectangle(top_left, "wide", 5)
        with self.assertRaises(TypeError):
            Rectangle(top_left, 10, "tall")


    def test_polygon_initialization(self):
        """Test Polygon class initialization."""
        points = [Point(0, 0), Point(1, 0), Point(1, 1)]
        polygon = Polygon(points)
        self.assertEqual(polygon.list_of_points, points)

        # Test invalid input
        with self.assertRaises(TypeError):
            Polygon("not a list")
        with self.assertRaises(TypeError):
            Polygon([Point(0,0), "not a point", Point(1,1)])
        with self.assertRaises(ValueError):
            Polygon([Point(0,0), Point(1,0)]) # Less than 3 points

    def test_distance(self):
        """Test the distance function."""
        p1 = Point(0, 0)
        p2 = Point(3, 4)
        self.assertAlmostEqual(distance(p1, p2), 5.0)

        # Test distance between the same point
        self.assertAlmostEqual(distance(p1, p1), 0.0)

        # Test with negative coordinates
        p3 = Point(-1, -1)
        p4 = Point(2, 3)
        self.assertAlmostEqual(distance(p3, p4), 5.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            distance(p1, 123)
        with self.assertRaises(TypeError):
            distance(456, p2)


    def test_line_length(self):
        """Test the line_length function."""
        p1 = Point(0, 0)
        p2 = Point(3, 4)
        line = Line(p1, p2)
        self.assertAlmostEqual(line_length(line), 5.0)

        # Test with a line of zero length
        line_zero = Line(p1, p1)
        self.assertAlmostEqual(line_length(line_zero), 0.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            line_length(123)

    def test_circle_area(self):
        """Test the circle_area function."""
        center = Point(0, 0)
        circle = Circle(center, 5)
        self.assertAlmostEqual(circle_area(circle), math.pi * 25)

        # Test circle with radius 0
        circle_zero = Circle(center, 0)
        self.assertAlmostEqual(circle_area(circle_zero), 0.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            circle_area(123)

    def test_circle_perimeter(self):
        """Test the circle_perimeter function."""
        center = Point(0, 0)
        circle = Circle(center, 5)
        self.assertAlmostEqual(circle_perimeter(circle), 2 * math.pi * 5)

        # Test circle with radius 0
        circle_zero = Circle(center, 0)
        self.assertAlmostEqual(circle_perimeter(circle_zero), 0.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            circle_perimeter(123)

    def test_rectangle_area(self):
        """Test the rectangle_area function."""
        top_left = Point(0, 0)
        rectangle = Rectangle(top_left, 10, 5)
        self.assertAlmostEqual(rectangle_area(rectangle), 50.0)

        # Test rectangle with zero width or height
        rectangle_zero_width = Rectangle(top_left, 0, 5)
        self.assertAlmostEqual(rectangle_area(rectangle_zero_width), 0.0)
        rectangle_zero_height = Rectangle(top_left, 10, 0)
        self.assertAlmostEqual(rectangle_area(rectangle_zero_height), 0.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            rectangle_area(123)

    def test_rectangle_perimeter(self):
        """Test the rectangle_perimeter function."""
        top_left = Point(0, 0)
        rectangle = Rectangle(top_left, 10, 5)
        self.assertAlmostEqual(rectangle_perimeter(rectangle), 30.0)

        # Test rectangle with zero width or height
        rectangle_zero_width = Rectangle(top_left, 0, 5)
        self.assertAlmostEqual(rectangle_perimeter(rectangle_zero_width), 10.0)
        rectangle_zero_height = Rectangle(top_left, 10, 0)
        self.assertAlmostEqual(rectangle_perimeter(rectangle_zero_height), 20.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            rectangle_perimeter(123)

    def test_polygon_area(self):
        """Test the polygon_area function."""
        # Square
        square_points = [Point(0, 0), Point(4, 0), Point(4, 4), Point(0, 4)]
        square = Polygon(square_points)
        self.assertAlmostEqual(polygon_area(square), 16.0)

        # Triangle
        triangle_points = [Point(0, 0), Point(3, 0), Point(0, 4)]
        triangle = Polygon(triangle_points)
        self.assertAlmostEqual(polygon_area(triangle), 6.0)

        # Degenerate polygon (collinear points)
        degenerate_points = [Point(0, 0), Point(1, 0), Point(2, 0)]
        degenerate_polygon = Polygon(degenerate_points)
        self.assertAlmostEqual(polygon_area(degenerate_polygon), 0.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            polygon_area(123)

    def test_polygon_perimeter(self):
        """Test the polygon_perimeter function."""
        # Square
        square_points = [Point(0, 0), Point(4, 0), Point(4, 4), Point(0, 4)]
        square = Polygon(square_points)
        self.assertAlmostEqual(polygon_perimeter(square), 16.0)

        # Triangle
        triangle_points = [Point(0, 0), Point(3, 0), Point(0, 4)]
        triangle = Polygon(triangle_points)
        self.assertAlmostEqual(polygon_perimeter(triangle), 12.0) # 3 + 4 + 5

        # Degenerate polygon (collinear points)
        degenerate_points = [Point(0, 0), Point(1, 0), Point(2, 0)]
        degenerate_polygon = Polygon(degenerate_points)
        self.assertAlmostEqual(polygon_perimeter(degenerate_polygon), 2.0) # 1 + 1 + 0

        # Test invalid input
        with self.assertRaises(TypeError):
            polygon_perimeter(123)

  ##Create the necessary directory structure and move the existing code and tests into the appropriate files and directories to prepare for packaging.



import os

# Create the root directory for the library
library_root_dir = "geometry_library_package"
os.makedirs(library_root_dir, exist_ok=True)

# Create the subdirectory for the library code
library_code_dir = os.path.join(library_root_dir, "geometry_library")
os.makedirs(library_code_dir, exist_ok=True)

# Create the tests directory
tests_dir = os.path.join(library_root_dir, "tests")
os.makedirs(tests_dir, exist_ok=True)

# Define the content of the geometry library code file
geometry_code = """
import math

class Point:
    \"\"\"
    Represents a point in 2D space.

    Attributes:
        x_coordinate (float): The x-coordinate of the point.
        y_coordinate (float): The y-coordinate of the point.

    Examples:
        >>> p = Point(5, 10)
        >>> p.x_coordinate
        5
        >>> p.y_coordinate
        10
    \"\"\"
    def __init__(self, x_coordinate, y_coordinate):
        self.x_coordinate = x_coordinate
        self.y_coordinate = y_coordinate

    def __repr__(self):
        return f"Point(x={self.x_coordinate}, y={self.y_coordinate})"

    def __eq__(self, other):
        if isinstance(other, Point):
            return self.x_coordinate == other.x_coordinate and self.y_coordinate == other.y_coordinate
        return False


class Line:
    \"\"\"
    Represents a line defined by two Point objects.

    Attributes:
        point1 (Point): The first Point object defining the line.
        point2 (Point): The second Point object defining the line.

    Raises:
        TypeError: If point1 or point2 are not Point objects.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(3, 4)
        >>> line = Line(p1, p2)
        >>> line.point1
        Point(x=0, y=0)
        >>> line.point2
        Point(x=3, y=4)
    \"\"\"
    def __init__(self, point1, point2):
        if not isinstance(point1, Point) or not isinstance(point2, Point):
            raise TypeError("Both point1 and point2 must be Point objects.")
        self.point1 = point1
        self.point2 = point2

    def __repr__(self):
        return f"Line(point1={self.point1}, point2={self.point2})"

class Circle:
    \"\"\"
    Represents a circle.

    Attributes:
        center_point (Point): The center Point object of the circle.
        radius (float): The radius of the circle.

    Raises:
        TypeError: If center_point is not a Point object.
        ValueError: If radius is not a non-negative number.

    Examples:
        >>> center = Point(0, 0)
        >>> circle = Circle(center, 5)
        >>> circle.center_point
        Point(x=0, y=0)
        >>> circle.radius
        5
        >>> Circle(center, -2)
        Traceback (most recent call last):
            ...
        ValueError: radius must be a non-negative number.
    \"\"\"
    def __init__(self, center_point, radius):
        if not isinstance(center_point, Point):
            raise TypeError("center_point must be a Point object.")
        if not isinstance(radius, (int, float)) or radius < 0:
            raise ValueError("radius must be a non-negative number.")
        self.center_point = center_point
        self.radius = radius

    def __repr__(self):
        return f"Circle(center={self.center_point}, radius={self.radius})"

class Rectangle:
    \"\"\"
    Represents a rectangle defined by its top-left corner, width, and height.

    Attributes:
        top_left_point (Point): The top-left Point object of the rectangle.
        width (float): The width of the rectangle.
        height (float): The height of the rectangle.

    Raises:
        TypeError: If top_left_point is not a Point object.
        ValueError: If width or height are not non-negative numbers.

    Examples:
        >>> top_left = Point(1, 5)
        >>> rectangle = Rectangle(top_left, 10, 5)
        >>> rectangle.top_left_point
        Point(x=1, y=5)
        >>> rectangle.width
        10
        >>> rectangle.height
        5
    \"\"\"
    def __init__(self, top_left_point, width, height):
        if not isinstance(top_left_point, Point):
            raise TypeError("top_left_point must be a Point object.")
        if not isinstance(width, (int, float)) or width < 0:
            raise ValueError("width must be a non-negative number.")
        if not isinstance(height, (int, float)) or height < 0:
            raise ValueError("height must be a non-negative number.")
        self.top_left_point = top_left_point
        self.width = width
        self.height = height

    def __repr__(self):
        return f"Rectangle(top_left={self.top_left_point}, width={self.width}, height={self.height})"

class Polygon:
    \"\"\"
    Represents a polygon defined by a list of Point objects.

    The points should be listed in order, either clockwise or counter-clockwise.

    Attributes:
        list_of_points (list[Point]): A list of Point objects defining the vertices of the polygon.

    Raises:
        TypeError: If list_of_points is not a list or contains non-Point objects.
        ValueError: If the number of points is less than 3.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(4, 0)
        >>> p3 = Point(4, 3)
        >>> p4 = Point(0, 3)
        >>> polygon = Polygon([p1, p2, p3, p4])
        >>> polygon.list_of_points
        [Point(x=0, y=0), Point(x=4, y=0), Point(x=4, y=3), Point(x=0, y=3)]
        >>> Polygon([p1, p2])
        Traceback (most recent call last):
            ...
        ValueError: A polygon must have at least 3 points.
    \"\"\"
    def __init__(self, list_of_points):
        if not isinstance(list_of_points, list) or not all(isinstance(p, Point) for p in list_of_points):
            raise TypeError("list_of_points must be a list of Point objects.")
        if len(list_of_points) < 3:
             raise ValueError("A polygon must have at least 3 points.")
        self.list_of_points = list_of_points

    def __repr__(self):
        return f"Polygon(points={self.list_of_points})"

def distance(point1, point2):
    \"\"\"
    Calculates the Euclidean distance between two Point objects.

    Args:
        point1 (Point): The first Point object.
        point2 (Point): The second Point object.

    Returns:
        float: The distance between the two points.

    Raises:
        TypeError: If point1 or point2 are not Point objects.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(3, 4)
        >>> distance(p1, p2)
        5.0
    \"\"\"
    if not isinstance(point1, Point) or not isinstance(point2, Point):
        raise TypeError("Both inputs must be Point objects.")
    return math.sqrt((point2.x_coordinate - point1.x_coordinate)**2 + (point2.y_coordinate - point1.y_coordinate)**2)

def line_length(line):
    \"\"\"
    Calculates the length of a Line object.

    Args:
        line (Line): The Line object.

    Returns:
        float: The length of the line.

    Raises:
        TypeError: If the input is not a Line object.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(3, 4)
        >>> line = Line(p1, p2)
        >>> line_length(line)
        5.0
    \"\"\"
    if not isinstance(line, Line):
        raise TypeError("Input must be a Line object.")
    return distance(line.point1, line.point2)

def circle_area(circle):
    \"\"\"
    Calculates the area of a Circle object.

    Args:
        circle (Circle): The Circle object.

    Returns:
        float: The area of the circle.

    Raises:
        TypeError: If the input is not a Circle object.

    Examples:
        >>> center = Point(0, 0)
        >>> circle = Circle(center, 5)
        >>> round(circle_area(circle), 2)
        78.54
    \"\"\"
    if not isinstance(circle, Circle):
        raise TypeError("Input must be a Circle object.")
    return math.pi * circle.radius**2

def circle_perimeter(circle):
    \"\"\"
    Calculates the perimeter (circumference) of a Circle object.

    Args:
        circle (Circle): The Circle object.

    Returns:
        float: The perimeter of the circle.

    Raises:
        TypeError: If the input is not a Circle object.

    Examples:
        >>> center = Point(0, 0)
        >>> circle = Circle(center, 5)
        >>> round(circle_perimeter(circle), 2)
        31.42
    \"\"\"
    if not isinstance(circle, Circle):
        raise TypeError("Input must be a Circle object.")
    return 2 * math.pi * circle.radius

def rectangle_area(rectangle):
    \"\"\"
    Calculates the area of a Rectangle object.

    Args:
        rectangle (Rectangle): The Rectangle object.

    Returns:
        float: The area of the rectangle.

    Raises:
        TypeError: If the input is not a Rectangle object.

    Examples:
        >>> top_left = Point(1, 5)
        >>> rectangle = Rectangle(top_left, 10, 5)
        >>> rectangle_area(rectangle)
        50
    \"\"\"
    if not isinstance(rectangle, Rectangle):
        raise TypeError("Input must be a Rectangle object.")
    return rectangle.width * rectangle.height

def rectangle_perimeter(rectangle):
    \"\"\"
    Calculates the perimeter of a Rectangle object.

    Args:
        rectangle (Rectangle): The Rectangle object.

    Returns:
        float: The perimeter of the rectangle.

    Raises:
        TypeError: If the input is not a Rectangle object.

    Examples:
        >>> top_left = Point(1, 5)
        >>> rectangle = Rectangle(top_left, 10, 5)
        >>> rectangle_perimeter(rectangle)
        30
    \"\"\"
    if not isinstance(rectangle, Rectangle):
        raise TypeError("Input must be a Rectangle object.")
    return 2 * (rectangle.width + rectangle.height)

def polygon_area(polygon):
    \"\"\"
    Calculates the area of a Polygon object using the shoelace formula.

    Args:
        polygon (Polygon): The Polygon object.

    Returns:
        float: The area of the polygon.

    Raises:
        TypeError: If the input is not a Polygon object.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(4, 0)
        >>> p3 = Point(4, 3)
        >>> p4 = Point(0, 3)
        >>> square = Polygon([p1, p2, p3, p4])
        >>> polygon_area(square)
        12.0
    \"\"\"
    if not isinstance(polygon, Polygon):
        raise TypeError("Input must be a Polygon object.")
    points = polygon.list_of_points
    n = len(points)
    area = 0.0
    for i in range(n):
        j = (i + 1) % n
        area += points[i].x_coordinate * points[j].y_coordinate
        area -= points[j].x_coordinate * points[i].y_coordinate
    area = abs(area) / 2.0
    return area

def polygon_perimeter(polygon):
    \"\"\"
    Calculates the perimeter of a Polygon object by summing the lengths of its sides.

    Args:
        polygon (Polygon): The Polygon object.

    Returns:
        float: The perimeter of the polygon.

    Raises:
        TypeError: If the input is not a Polygon object.

    Examples:
        >>> p1 = Point(0, 0)
        >>> p2 = Point(4, 0)
        >>> p3 = Point(4, 3)
        >>> p4 = Point(0, 3)
        >>> square = Polygon([p1, p2, p3, p4])
        >>> polygon_perimeter(square)
        14.0
        >>> triangle = Polygon([Point(0,0), Point(3,0), Point(0,4)])
        >>> polygon_perimeter(triangle)
        12.0
    \"\"\"
    if not isinstance(polygon, Polygon):
        raise TypeError("Input must be a Polygon object.")
    points = polygon.list_of_points
    n = len(points)
    perimeter = 0.0
    for i in range(n):
        j = (i + 1) % n
        perimeter += distance(points[i], points[j])
    return perimeter
"""

# Define the content of the test file
test_code = """
import unittest
import math
from geometry_library.geometry import Point, Line, Circle, Rectangle, Polygon, distance, line_length, circle_area, circle_perimeter, rectangle_area, rectangle_perimeter, polygon_area, polygon_perimeter

class TestGeometry(unittest.TestCase):
    \"\"\"Unit tests for the geometry library.\"\"\"

    def test_point_initialization(self):
        \"\"\"Test Point class initialization.\"\"\"
        p = Point(10, 20)
        self.assertEqual(p.x_coordinate, 10)
        self.assertEqual(p.y_coordinate, 20)

    def test_line_initialization(self):
        \"\"\"Test Line class initialization.\"\"\"
        p1 = Point(0, 0)
        p2 = Point(1, 1)
        line = Line(p1, p2)
        self.assertEqual(line.point1, p1)
        self.assertEqual(line.point2, p2)

        # Test invalid input
        with self.assertRaises(TypeError):
            Line(p1, 123)
        with self.assertRaises(TypeError):
            Line(456, p2)

    def test_circle_initialization(self):
        \"\"\"Test Circle class initialization.\"\"\"
        center = Point(0, 0)
        circle = Circle(center, 5)
        self.assertEqual(circle.center_point, center)
        self.assertEqual(circle.radius, 5)

        # Test invalid input
        with self.assertRaises(TypeError):
            Circle(123, 5)
        with self.assertRaises(ValueError):
            Circle(center, -2)
        with self.assertRaises(TypeError):
            Circle(center, "large")

    def test_rectangle_initialization(self):
        \"\"\"Test Rectangle class initialization.\"\"\"
        top_left = Point(1, 5)
        rectangle = Rectangle(top_left, 10, 5)
        self.assertEqual(rectangle.top_left_point, top_left)
        self.assertEqual(rectangle.width, 10)
        self.assertEqual(rectangle.height, 5)

        # Test invalid input
        with self.assertRaises(TypeError):
            Rectangle(123, 10, 5)
        with self.assertRaises(ValueError):
            Rectangle(top_left, -10, 5)
        with self.assertRaises(ValueError):
            Rectangle(top_left, 10, -5)
        with self.assertRaises(TypeError):
            Rectangle(top_left, "wide", 5)
        with self.assertRaises(TypeError):
            Rectangle(top_left, 10, "tall")


    def test_polygon_initialization(self):
        \"\"\"Test Polygon class initialization.\"\"\"
        points = [Point(0, 0), Point(1, 0), Point(1, 1)]
        polygon = Polygon(points)
        self.assertEqual(polygon.list_of_points, points)

        # Test invalid input
        with self.assertRaises(TypeError):
            Polygon("not a list")
        with self.assertRaises(TypeError):
            Polygon([Point(0,0), "not a point", Point(1,1)])
        with self.assertRaises(ValueError):
            Polygon([Point(0,0), Point(1,0)]) # Less than 3 points

    def test_distance(self):
        \"\"\"Test the distance function.\"\"\"
        p1 = Point(0, 0)
        p2 = Point(3, 4)
        self.assertAlmostEqual(distance(p1, p2), 5.0)

        # Test distance between the same point
        self.assertAlmostEqual(distance(p1, p1), 0.0)

        # Test with negative coordinates
        p3 = Point(-1, -1)
        p4 = Point(2, 3)
        self.assertAlmostEqual(distance(p3, p4), 5.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            distance(p1, 123)
        with self.assertRaises(TypeError):
            distance(456, p2)


    def test_line_length(self):
        \"\"\"Test the line_length function.\"\"\"
        p1 = Point(0, 0)
        p2 = Point(3, 4)
        line = Line(p1, p2)
        self.assertAlmostEqual(line_length(line), 5.0)

        # Test with a line of zero length
        line_zero = Line(p1, p1)
        self.assertAlmostEqual(line_length(line_zero), 0.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            line_length(123)

    def test_circle_area(self):
        \"\"\"Test the circle_area function.\"\"\"
        center = Point(0, 0)
        circle = Circle(center, 5)
        self.assertAlmostEqual(circle_area(circle), math.pi * 25)

        # Test circle with radius 0
        circle_zero = Circle(center, 0)
        self.assertAlmostEqual(circle_area(circle_zero), 0.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            circle_area(123)

    def test_circle_perimeter(self):
        \"\"\"Test the circle_perimeter function.\"\"\"
        center = Point(0, 0)
        circle = Circle(center, 5)
        self.assertAlmostEqual(circle_perimeter(circle), 2 * math.pi * 5)

        # Test circle with radius 0
        circle_zero = Circle(center, 0)
        self.assertAlmostEqual(circle_perimeter(circle_zero), 0.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            circle_perimeter(123)

    def test_rectangle_area(self):
        \"\"\"Test the rectangle_area function.\"\"\"
        top_left = Point(0, 0)
        rectangle = Rectangle(top_left, 10, 5)
        self.assertAlmostEqual(rectangle_area(rectangle), 50.0)

        # Test rectangle with zero width or height
        rectangle_zero_width = Rectangle(top_left, 0, 5)
        self.assertAlmostEqual(rectangle_area(rectangle_zero_width), 0.0)
        rectangle_zero_height = Rectangle(top_left, 10, 0)
        self.assertAlmostEqual(rectangle_area(rectangle_zero_height), 0.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            rectangle_area(123)

    def test_rectangle_perimeter(self):
        \"\"\"Test the rectangle_perimeter function.\"\"\"
        top_left = Point(0, 0)
        rectangle = Rectangle(top_left, 10, 5)
        self.assertAlmostEqual(rectangle_perimeter(rectangle), 30.0)

        # Test rectangle with zero width or height
        rectangle_zero_width = Rectangle(top_left, 0, 5)
        self.assertAlmostEqual(rectangle_perimeter(rectangle_zero_width), 10.0)
        rectangle_zero_height = Rectangle(top_left, 10, 0)
        self.assertAlmostEqual(rectangle_perimeter(rectangle_zero_height), 20.0)
         # Test invalid input
        with self.assertRaises(TypeError):
            rectangle_perimeter(123)

    def test_polygon_area(self):
        \"\"\"Test the polygon_area function.\"\"\"
        # Square
        square_points = [Point(0, 0), Point(4, 0), Point(4, 4), Point(0, 4)]
        square = Polygon(square_points)
        self.assertAlmostEqual(polygon_area(square), 16.0)

        # Triangle
        triangle_points = [Point(0, 0), Point(3, 0), Point(0, 4)]
        triangle = Polygon(triangle_points)
        self.assertAlmostEqual(polygon_area(triangle), 6.0)

        # Degenerate polygon (collinear points)
        degenerate_points = [Point(0, 0), Point(1, 0), Point(2, 0)]
        degenerate_polygon = Polygon(degenerate_points)
        self.assertAlmostEqual(polygon_area(degenerate_polygon), 0.0)

        # Test invalid input
        with self.assertRaises(TypeError):
            polygon_area(123)

    def test_polygon_perimeter(self):
        \"\"\"Test the polygon_perimeter function.\"\"\"
        # Square
        square_points = [Point(0, 0), Point(4, 0), Point(4, 4), Point(0, 4)]
        square = Polygon(square_points)
        self.assertAlmostEqual(polygon_perimeter(square), 16.0)

        # Triangle
        triangle_points = [Point(0, 0), Point(3, 0), Point(0, 4)]
        triangle = Polygon(triangle_points)
        self.assertAlmostEqual(polygon_perimeter(triangle), 12.0) # 3 + 4 + 5

        # Degenerate polygon (collinear points)
        degenerate_points = [Point(0, 0), Point(1, 0), Point(2, 0)]
        degenerate_polygon = Polygon(degenerate_points)
        self.assertAlmostEqual(polygon_perimeter(degenerate_polygon), 2.0) # 1 + 1 + 0

        # Test invalid input
        with self.assertRaises(TypeError):
            polygon_perimeter(123)

# To run the tests from the command line:
# python -m unittest tests/test_geometry.py
"""

# Write the geometry code to a file
geometry_file_path = os.path.join(library_code_dir, "geometry.py")
with open(geometry_file_path, "w") as f:
    f.write(geometry_code)

# Create the __init__.py file
init_file_path = os.path.join(library_code_dir, "__init__.py")
with open(init_file_path, "w") as f:
    f.write("") # This makes the directory a Python package

# Write the test code to a file
test_file_path = os.path.join(tests_dir, "test_geometry.py")
with open(test_file_path, "w") as f:
    f.write(test_code)

print(f"Created directory structure and files in '{library_root_dir}/'")
print(f"- {library_code_dir}/geometry.py")
print(f"- {library_code_dir}/__init__.py")
print(f"- {tests_dir}/test_geometry.py")


    

