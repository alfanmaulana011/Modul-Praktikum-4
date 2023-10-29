# Modul Praktikum 4 Teknik Pencarian Blind Search
# Alfan Maulana
# 5311421011
# Teknik Elektro

Modul Praktikum 4 - TEKNIK PENCARIAN BLIND SEARCH
1.	Tentukan bagaimana algoritma BFS berikut dapat menentukan node ke 8, 6, dan 7.
import java.util.ArrayDeque; 
import java.util.ArrayList; 
import java.util.HashMap; 
import java.util.List; 
import java.util.Map; 
import java.util.Queue; 
import java.util.Set; 
 
public class AdjacencyList 
{ 
public enum NodeColour { WHITE, GRAY, BLACK } 
public static class Node 
{ 
int data; 
int distance; 
NodeColour colour; 
public Node(int data) 
{ 
            this.data = data; 
        } 
        
    /**
     *
     * @return
     */
    @Override
        public String toString() 
        { 
         return "(" + data + ",d=" + distance + ")"; 
        } 
    } 
    
    Map<Node, List<Node>> nodes; 
 
    public AdjacencyList() 
    { 
        nodes = new HashMap<>(); 
    } 
    
    public void addEdge(Node n1, Node n2) 
    { 
        if (nodes.containsKey(n1)) { 
            nodes.get(n1).add(n2); 
        } else { 
       ArrayList<Node> list = new ArrayList<>(); 
            list.add(n2); 
            nodes.put(n1, list); 
        } 
    } 
    
    public void bfs(Node s) 
    { 
        Set<Node> keys = nodes.keySet(); 
        for (Node u : keys) { 
            if (u != s) { 
                u.colour = NodeColour.WHITE; 
                u.distance = Integer.MAX_VALUE; 
            } 
        } 
        s.colour = NodeColour.GRAY; 
        s.distance = 0; 
        Queue<Node> q = new ArrayDeque<>(); 
        q.add(s); 
        while (!q.isEmpty()) { 
            Node u = q.remove(); 
            List<Node> adj_u = nodes.get(u); 
            if (adj_u != null) { 
                for (Node v : adj_u) { 
                    if(v.colour == NodeColour.WHITE) { 
                        v.colour = NodeColour.GRAY; 
                        v.distance = u.distance + 1; 
                        q.add(v); 
                    } 
                } 
            } 
            u.colour = NodeColour.BLACK; 
            System.out.print(u + " "); 
        } 
    } 
    public static void main(String[] args)
     { 
        AdjacencyList graph = new AdjacencyList(); 
        Node n1 = new Node(1); 
        Node n2 = new Node(2); 
        Node n3 = new Node(3); 
        Node n4 = new Node(4); 
        Node n5 = new Node(5); 
        Node n6 = new Node(6); 
        Node n7 = new Node(7); 
        Node n8 = new Node(8); 
        
        graph.addEdge(n1, n2); 
        
        graph.addEdge(n2, n1); 
        graph.addEdge(n2, n3); 
        
        graph.addEdge(n3, n4); 
        graph.addEdge(n3, n2); 
        
        graph.addEdge(n4, n3); 
        graph.addEdge(n4, n5); 
        graph.addEdge(n4, n6); 
        
        graph.addEdge(n5, n4); 
        graph.addEdge(n5, n6); 
        graph.addEdge(n5, n7); 
        
        graph.addEdge(n6, n4); 
        graph.addEdge(n6, n5); 
        graph.addEdge(n6, n7); 
        graph.addEdge(n6, n8); 
        
        graph.addEdge(n7, n5); 
        graph.addEdge(n7, n6); 
        graph.addEdge(n7, n8); 
        
        graph.addEdge(n8, n6); 
        graph.addEdge(n8, n7); 
        
        graph.bfs(n3); 
 
    } 
}

Jawab:
Setelah melakukan praktikum dengan menggunakan software NetBeans dan menjalankan program sesuai pada Modul 4, maka didapatkan hasil seperti berikut:
(3,d=0) (4,d=1) (2,d=1) (5,d=2) (6,d=2) (1,d=2) (7,d=3) (8,d=3)


Perlu diketahui bahwa Algoritma Breadth-First Search (BFS) digunakan untuk menjelajahi atau mencari jalur terpendek dari satu simpul (node) ke simpul lain dalam graf. Pada program di atas, BFS dimulai dari simpul (node) ke-3 (n3).

Dalam langkah-langkah pencarian menggunakan algoritma Breadth-First Search (BFS) pada graf ini, pencarian dimulai dari node awal atau inisial state, yaitu node 3 dengan jarak 0. Setelah itu, BFS menemukan node 4 dengan jarak 1, lalu melanjutkan ke node 2 dengan jarak yang sama. Node 5 ditemukan pada jarak 2 dan dari sana BFS mencapai node 6 dan 1 dengan jarak yang sama. Selanjutnya, pencarian berlanjut ke node 7 dengan jarak 3 melalui node 6. Akhirnya, BFS juga mencapai node 8 pada jarak 3 melalui node 6 yang masih berada dalam proses pencarian. Dengan demikian, algoritma BFS berhasil menemukan node 8, 6, dan 7 dengan jarak masing-masing 3 langkah dari node awal atau inisial state, yaitu node 3.

2.	Ubahlah method static void main sehingga bentuk tree seperti Gambar 4.5 dapat dibentuk. Kemudian tentukan bagaimana algoritma BFS dapat menemukan node 5.
Jawab:
import java.util.ArrayDeque; 
import java.util.ArrayList; 
import java.util.HashMap; 
import java.util.List; 
import java.util.Map; 
import java.util.Queue; 
import java.util.Set; 

public class AdjacencyList 
{ 
public enum NodeColour { WHITE, GRAY, BLACK } 
public static class Node 
{ 
int data; 
int distance; 
NodeColour colour; 
public Node(int data) 
{ 
            this.data = data; 
        } 
        
    /**
     *
     * @return
     */
    @Override
        public String toString() 
        { 
         return "(" + data + ",d=" + distance + ")"; 
        } 
    } 
    
    Map<Node, List<Node>> nodes; 
 
    public AdjacencyList() 
    { 
        nodes = new HashMap<>(); 
    } 
    
    public void addEdge(Node n1, Node n2) 
    { 
        if (nodes.containsKey(n1)) { 
            nodes.get(n1).add(n2); 
        } else { 
       ArrayList<Node> list = new ArrayList<>(); 
            list.add(n2); 
            nodes.put(n1, list); 
        } 
    } 
    
    public void bfs(Node s) 
    { 
        Set<Node> keys = nodes.keySet(); 
        for (Node u : keys) { 
            if (u != s) { 
                u.colour = NodeColour.WHITE; 
                u.distance = Integer.MAX_VALUE; 
            } 
        } 
        s.colour = NodeColour.GRAY; 
        s.distance = 0; 
        Queue<Node> q = new ArrayDeque<>(); 
        q.add(s); 
        while (!q.isEmpty()) { 
            Node u = q.remove(); 
            List<Node> adj_u = nodes.get(u); 
            if (adj_u != null) { 
                for (Node v : adj_u) { 
                    if(v.colour == NodeColour.WHITE) { 
                        v.colour = NodeColour.GRAY; 
                        v.distance = u.distance + 1; 
                        q.add(v); 
                    } 
                } 
            } 
            u.colour = NodeColour.BLACK; 
            System.out.print(u + " "); 
        } 
    } 
    public static void main(String[] args) { 
    AdjacencyList graph = new AdjacencyList(); 
    Node n0 = new Node(0); 
    Node n1 = new Node(1); 
    Node n2 = new Node(2); 
    Node n3 = new Node(3); 
    Node n4 = new Node(4); 
    Node n5 = new Node(5); 
    Node n6 = new Node(6); 
    
    graph.addEdge(n0, n1); 
    graph.addEdge(n0, n2); 
    graph.addEdge(n1, n0); 
    graph.addEdge(n1, n3); 
    graph.addEdge(n1, n4); 
    graph.addEdge(n2, n0); 
    graph.addEdge(n2, n5); 
    graph.addEdge(n2, n6); 
    graph.addEdge(n3, n1); 
    graph.addEdge(n3, n4);
    graph.addEdge(n4, n3); 
    graph.addEdge(n4, n1);
    graph.addEdge(n5, n2); 
    graph.addEdge(n5, n6);
    graph.addEdge(n5, n1); 
    graph.addEdge(n6, n2);
    graph.addEdge(n6, n5); 
    graph.addEdge(n6, n1);
    
    
    graph.bfs(n0); 
    }
}

Hasil: (0,d=0) (1,d=1) (2,d=1) (3,d=2) (4,d=2) (5,d=2) (6,d=2)

Program diatas telah diubah sesuai dengan bentuk Gambar 4.5 Tree 1 yang terdapat pada Modul 4. Untuk menemukan node 5, algoritma BFS melakukan pencarian dimulai dari inisial state, yaitu node 0 yang memiliki dua anak cabang, yaitu Node 1 dan Node 2. BFS memulai pencarian dengan melanjutkan ke Node 1 yang memiliki dua anak cabang, yaitu Node 3 dan Node 4. Namun, saat mencapai Node 4, BFS tidak menemukan Node 5 dalam proses BFS sehingga setelah mengeksplorasi anak-anak cabang dari Node 1, BFS kembali ke Node 0 dan melanjutkan ke Node 2 yang memiliki anak Node 5. Akhirnya, BFS menemukan Node 5 dengan jarak 2 dari Node awal atau inisial state, yaitu Node 0.

3.	Ubahlah method static void main sehingga bentuk tree seperti Gambar 4.6 dapat dibentuk. Kemudian tentukan bagaimana algoritma BFS dapat menemukan node 9.
Jawab:
import java.util.ArrayDeque; 
import java.util.ArrayList; 
import java.util.HashMap; 
import java.util.List; 
import java.util.Map; 
import java.util.Queue; 
import java.util.Set; 

public class AdjacencyList 
{ 
public enum NodeColour { WHITE, GRAY, BLACK } 
public static class Node 
{ 
int data; 
int distance; 
NodeColour colour; 
public Node(int data) 
{ 
            this.data = data; 
        } 
        
    /**
     *
     * @return
     */
    @Override
        public String toString() 
        { 
         return "(" + data + ",d=" + distance + ")"; 
        } 
    } 
    
    Map<Node, List<Node>> nodes; 
 
    public AdjacencyList() 
    { 
        nodes = new HashMap<>(); 
    } 
    
    public void addEdge(Node n1, Node n2) 
    { 
        if (nodes.containsKey(n1)) { 
            nodes.get(n1).add(n2); 
        } else { 
       ArrayList<Node> list = new ArrayList<>(); 
            list.add(n2); 
            nodes.put(n1, list); 
        } 
    } 
    
    public void bfs(Node s) 
    { 
        Set<Node> keys = nodes.keySet(); 
        for (Node u : keys) { 
            if (u != s) { 
                u.colour = NodeColour.WHITE; 
                u.distance = Integer.MAX_VALUE; 
            } 
        } 
        s.colour = NodeColour.GRAY; 
        s.distance = 0; 
        Queue<Node> q = new ArrayDeque<>(); 
        q.add(s); 
        while (!q.isEmpty()) { 
            Node u = q.remove(); 
            List<Node> adj_u = nodes.get(u); 
            if (adj_u != null) { 
                for (Node v : adj_u) { 
                    if(v.colour == NodeColour.WHITE) { 
                        v.colour = NodeColour.GRAY; 
                        v.distance = u.distance + 1; 
                        q.add(v); 
                    } 
                } 
            } 
            u.colour = NodeColour.BLACK; 
            System.out.print(u + " "); 
        } 
    } 
    public static void main(String[] args) { 
    AdjacencyList graph = new AdjacencyList(); 
    Node n1 = new Node(1); 
    Node n2 = new Node(2); 
    Node n3 = new Node(3); 
    Node n4 = new Node(4); 
    Node n5 = new Node(5); 
    Node n6 = new Node(6); 
    Node n7 = new Node(7); 
    Node n8 = new Node(8); 
    Node n9 = new Node(9); 
    Node n10 = new Node(10); 
    Node n11 = new Node(11); 
    Node n12 = new Node(12); 
    
    graph.addEdge(n1, n2); 
    graph.addEdge(n1, n3); 
    graph.addEdge(n1, n4); 
    graph.addEdge(n2, n1); 
    graph.addEdge(n2, n5); 
    graph.addEdge(n2, n6); 
    graph.addEdge(n3, n1); 
    graph.addEdge(n4, n1);
    graph.addEdge(n4, n7); 
    graph.addEdge(n4, n8);
    graph.addEdge(n5, n2); 
    graph.addEdge(n5, n9);
    graph.addEdge(n5, n10); 
    graph.addEdge(n5, n6);
    graph.addEdge(n6, n2); 
    graph.addEdge(n6, n5);
    graph.addEdge(n7, n4); 
    graph.addEdge(n7, n11); 
    graph.addEdge(n7, n12); 
    graph.addEdge(n7, n8); 
    graph.addEdge(n8, n4);
    graph.addEdge(n8, n7); 
    graph.addEdge(n9, n5);
    graph.addEdge(n9, n10); 
    graph.addEdge(n10, n5);
    graph.addEdge(n10, n9); 
    graph.addEdge(n11, n7);
    graph.addEdge(n11, n12); 
    graph.addEdge(n12, n7);
    graph.addEdge(n12, n11);    
    
    graph.bfs(n1); 
    }
}

Hasil: (1,d=0) (2,d=1) (3,d=1) (4,d=1) (5,d=2) (6,d=2) (7,d=2) (8,d=2) (9,d=3) (10,d=3) (11,d=3) (12,d=3)

Program diatas telah diubah sesuai bentuk Gambar 4.6 Tree 2 yang terdapat pada Modul 4. Untuk menemukan Node 9, algoritma BFS melakukan pencarian dimulai dari node 1 (n1) sebagai node awal atau inisial state. Kemudian, BFS mengeksplorasi cabang anak-anak dari inisial state 1, yaitu node 2, node 3, dan node 4. Namun, karena node 3 dan node 4 sudah diwarnai GRAY saat proses BFS, pencarian tidak melanjutkan eksplorasi pada node-node tersebut. BFS melanjutkan ke simpul 2, yang memiliki dua anak cabang, yaitu node 5 dan node 6. Node 5 kemudian dijelajahi lebih dalam. Node 5 memiliki dua anak cabang, yaitu node 9 dan node 10. Algoritma BFS terus melanjutkan pencarian hingga menemukan node 9 dengan jarak 3 dari inisial state, yaitu 1. Dengan langkah-langkah ini, BFS berhasil menemukan simpul 9 dalam graf dengan menggunakan pendekatan berlapis yang karakteristik dari algoritma Breadth-First Search.

4.	Ubahlah kode program di atas sehingga bentuk tree seperti Gambar 4.7 Tree 3 dapat dibentuk. Kemudian tentukan bagaimana algoritma BFS dapat menemukan node C.
Jawab:
import java.util.ArrayDeque; 
import java.util.ArrayList; 
import java.util.HashMap; 
import java.util.List; 
import java.util.Map; 
import java.util.Queue; 
import java.util.Set; 

public class AdjacencyList 
{ 
public enum NodeColour { WHITE, GRAY, BLACK } 
public static class Node 
{ 
char data; 
int distance; 
NodeColour colour; 
public Node(int data) 
{ 
            this.data = (char) data; 
        } 
        
    /**
     *
     * @return
     */
    @Override
        public String toString() 
        { 
         return "(" + data + ",d=" + distance + ")"; 
        } 
    } 
    
    Map<Node, List<Node>> nodes; 
 
    public AdjacencyList() 
    { 
        nodes = new HashMap<>(); 
    } 
    
    public void addEdge(Node n1, Node n2) 
    { 
        if (nodes.containsKey(n1)) { 
            nodes.get(n1).add(n2); 
        } else { 
       ArrayList<Node> list = new ArrayList<>(); 
            list.add(n2); 
            nodes.put(n1, list); 
        } 
    } 
    
    public void bfs(Node s) 
    { 
        Set<Node> keys = nodes.keySet(); 
        for (Node u : keys) { 
            if (u != s) { 
                u.colour = NodeColour.WHITE; 
                u.distance = Integer.MAX_VALUE; 
            } 
        } 
        s.colour = NodeColour.GRAY; 
        s.distance = 0; 
        Queue<Node> q = new ArrayDeque<>(); 
        q.add(s); 
        while (!q.isEmpty()) { 
            Node u = q.remove(); 
            List<Node> adj_u = nodes.get(u); 
            if (adj_u != null) { 
                for (Node v : adj_u) { 
                    if(v.colour == NodeColour.WHITE) { 
                        v.colour = NodeColour.GRAY; 
                        v.distance = u.distance + 1; 
                        q.add(v); 
                    } 
                } 
            } 
            u.colour = NodeColour.BLACK; 
            System.out.print(u + " "); 
        } 
    } 
    public static void main(String[] args) { 
    AdjacencyList graph = new AdjacencyList(); 
    Node n1 = new Node('A'); 
    Node n2 = new Node('B'); 
    Node n3 = new Node('C'); 
    Node n4 = new Node('D'); 
    Node n5 = new Node('E'); 
    Node n6 = new Node('F'); 
    Node n7 = new Node('G'); 
    Node n8 = new Node('H'); 
    Node n9 = new Node('I'); 
    
    
    graph.addEdge(n1, n2); 
    graph.addEdge(n1, n4); 
    graph.addEdge(n2, n6); 
    graph.addEdge(n2, n1); 
    graph.addEdge(n2, n4); 
    graph.addEdge(n3, n4); 
    graph.addEdge(n3, n5);
    graph.addEdge(n4, n2); 
    graph.addEdge(n4, n3);
    graph.addEdge(n4, n5); 
    graph.addEdge(n5, n4);
    graph.addEdge(n5, n3); 
    graph.addEdge(n6, n2);
    graph.addEdge(n6, n7); 
    graph.addEdge(n7, n6);
    graph.addEdge(n7, n9); 
    graph.addEdge(n8, n9); 
    graph.addEdge(n9, n8); 
      
    
    graph.bfs(n6); 
    }
}

Hasil: (F,d=0) (B,d=1) (G,d=1) (A,d=2) (D,d=2) (I,d=2) (C,d=3) (E,d=3) (H,d=3)

Saat BFS dimulai node 'F' sebagai inisial state. Selanjutnya, BFS melanjutkan pencarian ke node tetangga 'F', yaitu node 'B' (n2), yang memiliki dua anak cabang yaitu node 'A' (n1) dan 'D' (n4). Node 'A' diberi jarak 2 karena terhubung dengan node 'B' dan berjarak 1 dari 'B'. Namun, node 'D' sudah diwarnai GRAY dalam proses BFS sebelumnya, sehingga tidak dimasukkan ke dalam antrian. Selanjutnya, BFS menjelajahi node 'I' (n9), yang berjarak 2 dari node 'F'. Akhirnya, BFS mencapai node 'C' (n3) dengan jarak 3 dari node awal 'F'. Dengan melalui serangkaian langkah-langkah ini, algoritma BFS berhasil menemukan simpul 'C' dalam graf yang diberikan dengan jarak 3 dari simpul awalnya.


