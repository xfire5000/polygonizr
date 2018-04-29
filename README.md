polygonizr
==========
**A jQuery plugin for creating a polygon mesh network bacgrkound**

## License
[Beerware License](LICENSE.md)

## Samples

### Initialization
Initializes the plugin on a jQuery DOM-element, in this case a DIV-node with an id "site-landing". The plugin creates a canvas which is by default absolute positioned, and inherits the size of the parent. This can be applied to any DOM-element on the page.

```javascript
    $('#site-landing').polygonizr();
```
To set options for the plugin on initialization, simply declare the option and pass its value. See below for a [list of possible settings](#Settings-and-Defaults).

```javascript
    $('#site-landing').polygonizr({
        nodeEase: 'linear'
    });
```

### For lulz and funz
Among the settings, you can also alter how the initial x and y coordinates are positioned of every mesh nodes to create any desired pattern. For example, the following two samples draws a circle and a archimedean spiral.

```javascript
    // Positions the initialized mesh nodes as a circle.
    $('#site-landing-circle').polygonizr({
        randomizePolygonMeshNetworkFormation: false,
        specifyPolygonMeshNetworkFormation: function (i) {
            var forEachNode = {
                // Full circle 400x400 in the center of the canvas.
                x: (this.canvasWidth / 2) + Math.cos(2 * Math.PI * i / this.numberOfNodes) * 400,
                y: (this.canvasHeight / 2) + Math.sin(2 * Math.PI * i / this.numberOfNodes) * 400
            };
            return forEachNode;
        }
    });

    // Positions the initialized mesh nodes as a spiral.
    $('#site-landing-spiral').polygonizr({
        randomizePolygonMeshNetworkFormation: false,
        specifyPolygonMeshNetworkFormation: function (i) {
            var forEachNode = {
                // Archimedean spiral, note that 30 in this example is taken randomly to modify distance between successive turnings.
                x: (this.canvasWidth / 2) + (30 * ((i * 30) * Math.PI / 180)) * Math.cos((i * 30) * Math.PI / 180),
                y: (this.canvasHeight / 2) + (30 * ((i * 30) * Math.PI / 180)) * Math.sin((i * 30) * Math.PI / 180)
            };
            return forEachNode;
        }
    });
```

## Settings and Defaults

```javascript
    // How long to pause in between new node-movements.
    restNodeMovements: 1,
    // When the cluster updates, this sets speed of nodes.
    duration: 3,
    // Define the maximum distance to move nodes.
    nodeMovementDistance: 100,
    // The number of node nodes to print out.
    numberOfNodes: 25,
    // Define the maximume size of each node dot.
    nodeDotSize: 2.5,
    // Sets the ease mode of the movement: linear, easeIn, easeOut, easeInOut, accelerateDecelerate.
    nodeEase: "easeOut",
    // If true, the nodes will descend into place on load.
    nodeFancyEntrance: false,
    // Makes the cluster forms an ellipse inspired formation, random if true.
    randomizePolygonMeshNetworkFormation: true,
    // Define a formula for how to initialize each node dot's position.
    specifyPolygonMeshNetworkFormation: function (i) {
        var forEachNode = {
            // Half a circle and randomized
            x: this.canvasWidth - ((this.canvasWidth / 2) + (this.canvasHeight / 2) * Math.cos(i * (2 * Math.PI / this.numberOfNodes))) * Math.random(),
            y: this.canvasHeight - (this.canvasHeight * (i / this.numberOfNodes))
        };
        return forEachNode;
    },
    // Number of relations between nodes.
    nodeRelations: 3,
    // The FPS for the whole canvas.
    animationFps: 30,
    // Sets the color of the node dots in the network (RGB).
    nodeDotColor: "240, 255, 250",
    // Sets the color of the node lines in the network (RGB).
    nodeLineColor: "240, 255, 250",
    // Sets the color of the filled triangles in the network (RGB).
    nodeFillColor: "240, 255, 250",
    // Sets the alpha level for the colors (1-0).
    nodeFillAlpha: 0.5,
    // Sets the alpha level for the lines (1-0).
    nodeLineAlpha: 0.5,
    // Sets the alpha level for the dots (1-0).
    nodeDotAlpha: 1.0,
    // Defines if the triangles in the network should be shown.
    nodeFillSapce: true,
    // Define if the active animation should glow or not (not CPU friendly).
    nodeGlowing: false,
    // Define the canvas size and css position.
    canvasWidth: $(this).width(),
    canvasHeight: $(this).height(),
    canvasPosition: "absolute"
```