Certainly! You can modify the JavaScript code to achieve this effect based on the distance between the cursor and each arrow. Here's an updated example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        .arrow {
            transition: transform 0.3s ease-in-out;
            will-change: transform;
        }
    </style>
    <title>Interactive Arrows</title>
</head>
<body>

<!-- Include your arrow SVG set here, each with the class 'arrow' -->

<script>
    const arrows = document.querySelectorAll('.arrow');

    document.addEventListener('mousemove', (event) => {
        arrows.forEach(arrow => {
            const arrowRect = arrow.getBoundingClientRect();
            const arrowCenterX = arrowRect.left + arrowRect.width / 2;
            const arrowCenterY = arrowRect.top + arrowRect.height / 2;

            const distance = Math.sqrt(
                Math.pow(event.clientX - arrowCenterX, 2) + 
                Math.pow(event.clientY - arrowCenterY, 2)
            );

            const scaleFactor = 1 + (1 - distance / 200); // You can adjust the factor as needed

            arrow.style.transform = `scale(${scaleFactor})`;
        });
    });

    document.addEventListener('mouseout', () => {
        arrows.forEach(arrow => {
            arrow.style.transform = 'scale(1)';
        });
    });
</script>

</body>
</html>
```

This code calculates the distance between the cursor and each arrow's center. The closer the cursor is, the larger the scaling factor, creating the desired effect of arrows closer to the cursor moving faster. Adjust the factor in the `scaleFactor` calculation to control the sensitivity of the effect.
