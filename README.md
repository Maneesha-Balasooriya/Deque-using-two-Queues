# Deque-using-two-Queues
Deque using two Queues


/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Main.java to edit this template
 */
package DequeUsingQueue;

/**
 *
 * @author user
 */

import java.util.LinkedList;
import java.util.Queue;

public class DequeueUsing2Queues {

public class DequeUsing2Queues {
    private Queue<Integer> queue1;
    private Queue<Integer> queue2;

    public DequeUsing2Queues() {
        queue1 = new LinkedList<>();
        queue2 = new LinkedList<>();
    }

    // Insert at the front of the deque
    public void pushFront(int value) {
        queue2.offer(value);  // Insert new element into queue2
        while (!queue1.isEmpty()) {
            queue2.offer(queue1.poll()); // Move all elements to queue2
        }
        // Swap queue references
        Queue<Integer> temp = queue1;
        queue1 = queue2;
        queue2 = temp;
    }

    // Insert at the back of the deque
    public void pushBack(int value) {
        queue1.offer(value);
    }

    // Remove from the front of the deque
    public int popFront() {
        if (queue1.isEmpty()) {
            throw new RuntimeException("Deque is empty");
        }
        return queue1.poll();
    }

    // Remove from the back of the deque
    public int popBack() {
        if (queue1.isEmpty()) {
            throw new RuntimeException("Deque is empty");
        }
        // Move all elements except last to queue2
        while (queue1.size() > 1) {
            queue2.offer(queue1.poll());
        }
        int removedElement = queue1.poll(); // Remove last element

        // Swap queue references
        Queue<Integer> temp = queue1;
        queue1 = queue2;
        queue2 = temp;

        return removedElement;
    }

    // Check if deque is empty
    public boolean isEmpty() {
        return queue1.isEmpty();
    }

    // Get the front element
    public int getFront() {
        if (queue1.isEmpty()) {
            throw new RuntimeException("Deque is empty");
        }
        return queue1.peek();
    }

    // Get the back element
    public int getBack() {
        if (queue1.isEmpty()) {
            throw new RuntimeException("Deque is empty");
        }
        // Move elements to queue2, find the last element
        while (!queue1.isEmpty()) {
            int val = queue1.poll();
            queue2.offer(val);
            if (queue1.isEmpty()) {
                // Swap queue references
                Queue<Integer> temp = queue1;
                queue1 = queue2;
                queue2 = temp;
                return val; // Return last element
            }
        }
        throw new RuntimeException("Deque is empty");
    }

    

    public static void main(String[] args) {
        // TODO code application logic here
        DequeUsing2Queues deque = new DequeUsing2Queues();

        deque.pushFront(10);
        deque.pushBack(20);
        deque.pushFront(5);
        deque.pushBack(25);

        System.out.println("Front element: " + deque.getFront()); // Output: 5
        System.out.println("Back element: " + deque.getBack());   // Output: 25

        System.out.println("Removed Front: " + deque.popFront()); // Output: 5
        System.out.println("Removed Back: " + deque.popBack());   // Output: 25

        System.out.println("Front element after pop: " + deque.getFront()); // Output: 10
        System.out.println("Back element after pop: " + deque.getBack());   // Output: 20
    }
    
}
}

