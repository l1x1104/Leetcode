[负载均衡器]()

```java
public class LoadBalancer {
    private HashMap<Integer, Integer> map;
    private ArrayList<Integer> list;
    private Random rand;
    public LoadBalancer() {
        this.map = new HashMap<Integer, Integer>();
        this.list = new ArrayList<Integer>();
        this.rand = new Random();
    }

    // @param server_id add a new server to the cluster 
    // @return void
    public void add(int server_id) {
        if(!map.containsKey(server_id)){
            list.add(server_id);
            map.put(server_id, list.size() - 1);    
        }
    }

    // @param server_id server_id remove a bad server from the cluster
    // @return void
    public void remove(int server_id) {
        if(map.containsKey(server_id)){
            int removeIdx = map.get(server_id);
            map.remove(server_id);
            int affectedServerId = list.get(list.size() - 1);
            map.put(affectedServerId, removeIdx);
            list.set(removeIdx, affectedServerId);
            list.remove(list.size() - 1);
        }
    }

    // @return pick a server in the cluster randomly with equal probability
    public int pick() {
        if(list.size() == 0){
            return -1;
        }
        int rand_idx = rand.nextInt(list.size());
        return list.get(rand_idx);
    } 
}
```
