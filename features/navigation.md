# Navigation

[Youtube](https://youtu.be/BS0XvzyTnwA)

The commonly accepted navigation standard for Lineage is "expanding" each subsequent level on demand. This involves requesting information about each subsequent level from the backend.

At [**Dwh.dev**](https://dwh.dev/), we took a different approach - dependency information is loaded to the client, allowing us to display the necessary number of levels instantly, rebuilding the graph as needed.

For user's convenience, small graphs (with up to 500 connections) can be displayed entirely. Large graphs are available for exploration only in parts because navigating large graphs is almost impossible.

Initially, through a search, you find the necessary object in the catalog and by clicking the "lineage" button, you enter the "group" of that object.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

The main object of the group is highlighted with a dashed border.

The lineage screen supports scaling, scrolling, various types of centering, and a mini-map. You can always return to the main object by clicking the first button in the button group, aligning it in the toolbar, or by the object name in the top right.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

To the left of the central object are **Upstream** objects; to the right, **Downstream** objects. **Upstream** objects may have violet circles on the right side of the object. The numbers in these circles indicate the number of objects in **Downstream** that do not belong to the current group. Similarly, there is a green circle on the left of **Downstream** objects, indicating the number of objects from **Upstream** outside this group.

To enter a group of objects on the screen, double-click on it. To go back, press ESC.

By default, 2 levels of lineage are displayed. You can change this value in the settings panel under **Stream Options**:

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

You can also quickly disable the display of all Upstream/Downstream levels in the toolbar with the **"Toggle stream length to 0"** buttons.

If you want to explore the graph in a "classic" mode, navigating through its levels by "expanding" them, there is a **"Custom Path"** mode for this purpose:

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

The labels on the edges of the graph show how many levels are hidden in this branch, the number of objects in the first level, and the total number of objects.

You can highlight only the objects that interest you at the moment:

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

When working with complex graphs, even in **"Custom Path"** mode, it can be challenging to orient oneself. Therefore, you can "straighten" the selected path using the **"Straighten the path"** button in the toolbar:

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Both of these modes also work at the column level:

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>
