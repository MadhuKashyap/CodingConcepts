### Given array of orders[orderId, timestamp], design efficient structure to fetch last 100 orders in O(1) time.
```
package org.example.array;

import java.util.ArrayList;
import java.util.List;

class Order {
    int orderId;
    long timestamp;
    Order(int orderId, long timestamp) {
        this.orderId = orderId;
        this.timestamp = timestamp;
    }
}
class OrderBuffer {
    final int capacity;
    Order[] order;
    int index = 0;
    private boolean isFull = false;
    public OrderBuffer(int capacity) {
        this.capacity = capacity;
        order = new Order[capacity];
    }
    public void add(Order ord) {
        order[index] = ord;
        index = (index + 1) % capacity;
        if (index == 0) isFull = true;
    }
    public List<Order> getLastOrder() {
        List<Order> result = new ArrayList<>();
        int elements = isFull ? capacity : index;
        for (int i = 0; i < elements; i++) {
            int pos = (index - elements + i + capacity) % capacity;
            result.add(order[pos]);
        }
        return result;
    }
}
public class Design {

}

```
