Stacks are every day objects where you can add and remove things from the stack, this action of putting items on and off are O(1) operations. Pushing and Popping, Last In First Out (LIFO). This is great for undo / redo functions, back and forward in the browser.

Queue's have the inverse Big O Notation as Linked Lists, they can append to the back of the queue lightning fast O(1) but are slower to add to the front of the queue O(N). First in First Out (FIFO)

Stacks & Queues are often built using Arrays or Linked Lists, but mainly the Array because the Swift Array has push and pop like functionality already built in.
