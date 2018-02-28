---
title: Razl - Tasks
layout: RazlLayout
---

# Razl

## Task List

The Task List displays a list of actions you would like Razl to perform, you can queue up and review tasks in the task list before executing them all or selecting a single task and executing it.

![](/Images/Razl-V4/task1.png)

As tasks are executed they are removed from the Task List.

### Available Tasks

Razl supports the following list of tasks:

| Copy All | Copy all items and it’s children from the source instance to the target instance. Copy all has a merge and overwrite option. Merge will merge existing items and create new items, it does not delete any  items from the target instance. Overwrite will do the same as merge but also delete any items that exist on the target machine but not on the source machine. Any missing parent items will also be copied. | 
| Copy Item | Copy a single item from the source instance to the target instance. Any missing parents will also be copied. | 
| Copy Version | Copy a specific item version from the source instance to the target instance. | 
| Delete Item | Removes the item from the specified instance. | 
| Move Item | Moves the item in the content tree on the target instance to the same location on the source instance. It will also merge any field differences. Any missing parents will also be copied. |
| Set Field Value | Copy the specified field value from the source instance to the target instance. | 
| Set Property Value | Copy the specified item property from the source instance to the target instance. | 

### Copy All and Lightning Mode

When you have added a copy all task to the task list, you may run the task in normal mode or lightning mode. In normal mode, all items are copied even if they are the same. In Lightning Mode, the Revision Id for both sides is compared and if it matches, the item is skipped. This makes lightning mode much quicker when there are only a few scattered differences between the two Sitecore content trees.

### Multi-Threaded Copy
Razl can use multiple threads to copy items from one server to another. This only happens during the **Copy All** task. Razl will not concurrently execute multiple tasks. The number of threads Razl uses to copy item is specified for each connection. This allows the user to match the number of threads to the performance charactistics of the server. 

It is important to not specify too many threads for a server, as too many threads will slow down the server, impacting the other users of the server. Too many threads can also cause the copy operation to perform poorly. Determining the number of threads a server can handle is usually done by trial and error since many factors can infleuence server performance. Our testing has shown that the default of 4 threads works well for most servers. Specifying more than 15 threads hasn't shown to be of much benefit. 

Another limiting factor to copy performance is the network bandwidth. Creating too many copy threads can saturate the network, causing poor performance.

### Removing Tasks

Tasks can be removed from the list by clicking the red 'x' next to a task:

![](/Images/Razl/task2.PNG)

### Reordering Tasks
Tasks can be reordered in the task list by clicking the up and down arrows that are shown when the task is selected in the task list.

![](/Images/Razl-V4/ReorderTasks.png)

### Running Tasks

Tasks can be run by clicking the buttons at the bottom of the screen:

![](/Images/Razl/task3.PNG)

* **Do All** - Runs all tasks in the task list
* **Do Selected** - Runs the selected task from the task list
* **Export Tasks** - Saves the connections to the Sitecore servers and the list of tasks as an executable script.

## Exporting Tasks
Razl supports exporting the task list as a Razl Script. This is done by clicking the Export Tasks button at the bottom of the Razl form. The exported .xml task list can be executed using the [razl script](http://hedgehogdevelopment.github.io/razl/script.html) mechanism.
