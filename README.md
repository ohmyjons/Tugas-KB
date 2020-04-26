


# Tugas Kecerdasan Buatan-F
_Dohan Pranata Wikanda 05111840000139_

Teknik Informatika - Fakultas Teknologi elektro dan Informatika Cerdas

Institut Teknologi Sepuluh Nopember Surabaya


## 8 Puzzle

### BFS
Source Code [8 Puzzle BFS](https://github.com/ohmyjons/Tugas-KB/tree/master/8Puzzle/BFS)

Dalam program ini, melakukan pencarian state yang benar untuk menyelesaikan 8 puzzle dengan metode `(Breadth First Search)`. Setelah elemen dimasukkan pada deque dengan cara `push_back` ,dilakukan pencarian secara bfs.
```
from queue import Queue
from puzzle import Puzzle


def breadth_first_search(initial_state):
    start_node = Puzzle(initial_state, None, None, 0)
    if start_node.goal_test():
        return start_node.find_solution()
    q = Queue()
    q.put(start_node)
    explored=[]
    while not(q.empty()):
        node=q.get()
        explored.append(node.state)
        children=node.generate_child()
        for child in children:
            if child.state not in explored:
                if child.goal_test():
                    return child.find_solution()
                q.put(child)
    return
```
Dalam algoritma BFS ini  merupakan algoritma untuk _traversing_ atau _searching_ tree dan hal ini dimulai dari _root_. Dan aplikasinya adalah memeriksa secara luas ke tiap kemungkinan yang ada pada kondisi sekarang. Maka dari itu, BFS menggunakan sistem FIFO (First In, First Out), sehingga pencarian hanya berdasarkan level per level ketika ada _path_ yang mungkin dilalui.

![Animasi BFS](https://www3.cs.stonybrook.edu/~skiena/combinatorica/animations/anim/bfs.gif)
dalam Menjalankan program yang saya buat terdapat dalam main.py dimana disana sudah terdapat kondisi puzzle yang dapat dinput dengan main goal seperti ini :
![Input dan Mian goal](https://1.bp.blogspot.com/-ib7cGKelQBQ/UJy1QD7dldI/AAAAAAAAAFA/iLG6DT9FBdk/s1600/AI8pzzle.JPG)
>dengan kondisi kotak yang kosng berarti "0"

Berikut ini adalah method yang terdapat dalam class `Puzzle_class.py` beserta penjelasan singkatnya:
  1. `generate_heuristic()` : Fungsi ini digunakan untuk menyelesaikan permasalahan ketika `step` yang ingin diambil terlalu banyak langkah dan diperlukan penyingkatan langkah dan memperpendek _time executed_, sehingga fungsi `generate_heuristic()` sangat diperlukan.
  2. `goal_test()` : Fungsi ini digunakan untuk memeriksa apakah _state-child_ sudah sama dengan `goal_state`. Jika berbeda, akan melakukan return value `false`.
  3. `find_legal_actions()` : Fungsi ini digunakan untuk melakukan filter arah mana yang bisa dipenuhi berdasarkan koordinat kotak 0. Jika koordinat 0 berada di pojok 8puzzle, maka ada arah yang tidak bisa dipenuhi. `i` menunjukkan kolom, sedangkan `j` menunjukkan baris.
  4. `generate_child()` : Fungsi ini digunakan untuk membuat _child_ pada queue/tree yang ingin dicari. Kemudian mencari state baru ketika action yang ada valid (lewat fungsi `find_legal_actions()`).
  5. `find_solution()` : Fungsi ini digunakan untuk menyimpan solusi dari semua _moves_ yang ada. Dimulai dari _parent_ hingga _leaf_ paling bawah.

### DFS
Source Code [8 Puzzle DFS](https://github.com/ohmyjons/Tugas-KB/tree/master/8Puzzle/DFS)
Dalam program ini, melakukan pencarian state yang benar untuk menyelesaikan 8 puzzle dengan metode `Depth First Search`, dimana dalam pencariannya memungkinkan untuk pencarian degan bergerak mundur, yang diimplementasikan dibawah ini. Maksud dari bergerak mundur ini menginisiasi state yang sudah dilintasi yang berarti _traversing_ atau _searching_ tree dan hal ini dimulai dari _root_. Dan aplikasinya adalah memeriksa secara dalam _path_ secara satu satu. Maka dari itu, DFS menggunakan sistem LIFO (Last In First Out) untuk bisa memeriksa tree/graph secara menyeluruh dan dalam.
Ilustrasi :
![BFS](https://www3.cs.stonybrook.edu/~skiena/combinatorica/animations/anim/dfs.gif)

 Untuk 8 Puzzle solver dengan algoritma DFS, saya menggunakan referensi dari [sini](https://github.com/speix/8-puzzle-solver) dengan sedikit modifikasi karena saya tidak memerlukan algoritma BFS, AST, dan IDA.
 
 Hampir sama dengan BFS, Target state atau _goal state_ untuk 8 Puzzle ini adalah 
  
  ![gambar state](https://miro.medium.com/max/351/1*IQ4oYMH3SCAriifZMdZA9w.png)
  
  Berikut ini adalah penjelasan dari tiap fungsi yang terdapat dalam `driver.py`:
  1. `dfs()` : Fungsi ini merupakan implementasi dari algoritma DFS sendiri, dengan menggunakan _stack_ didalamnya dan menandai node yang telah dikunjungi dengan variabel `explored`. 
  2. `expand()` : Fungsi ini digunakan untuk menjumlahkan berapa banyak nodes yang telah diperluas (_nodes expanded_). Hasil dari _nodes expanded_ akan diprint oleh fungsi `export()`.
  3. `move()` : Fungsi ini digunakan untuk memindahkan posisi dari angka di board, dengan movement _Up_, _Down_, _Left_, _Right_ dan juga untuk melakukan update state baru ketika sudah melakukan giliran.
  4. `backtrace()` : Fungsi ini dijalankan ketika algoritma DFS telah selesai. Tujuannya adalah mengidentifikasi moves apa saja yang telah dilakukan, menamainya, kemudian memasukkan list moves tadi untuk kemudian dilakukan print oleh fungsi `export()`.
  5. `export()` : Fungsi ini untuk membuat file `output.txt`, yang berisi "Jalan/path", "Nodes yang diexpand", dan "Waktu Algoritma berjalan".
  6. `read()` : Fungsi ini digunakan untuk memisah state awal (pada argumen saat menjalankan program), menyimpan state awal di `initial_state`, mencari panjang board, dan mencari ukuran board.
  7. `main()` : Fungsi ini digunakan untuk run aplikasi dari awal dengan langkah-langkah sebagai berikut:
    a. Memisahkan argumen `algoritm` yang ingin dipakai dan `board` yang ingin diproses.
    b. Menghitung waktu ketika program dimulai
    c. Memproses `initial_state` dengan algoritma yang dipakai
    d. Menghitung waktu ketika fungsi `dfs()` selesai memproses `initial_state`
    3. Menjalankan fungsi `export()` dengan argumen hasil fungsi `dfs()` dan selisih waktu fungsi `dfs()` berjalan.
  
  File `state.py` digunakan sebagai class `State` untuk object yang akan digunakan pada Stack yang digunakan oleh algoritma DFS.

### IDS
Source Code [8 Puzzle IDS](https://github.com/ohmyjons/Tugas-KB/blob/master/8Puzzle/IDS/IDS.py)

IDS (_Iterative Deepening Search_) merupakan algoritma lanjutan dari DFS dengan menerapkan konsep yang sama dengan DFS. Tetapi, _improvement_-nya adalah IDS tidak mencari semua jalur seperti DFS, tetapi dicari secara _iterative_ berdasarkan level.
```
def ids():
  global inp
  global out
  global flag

  for limit in range(100):
    print('LIMIT -> '+str(limit))
    stack=[]
    inpx=[inp,"none"]
    stack.append(inpx)
    # for i in range(9):
    level=0
    while(True):
      if len(stack)==0:
        break
      puzzle=stack.pop(0)
      if level<=limit:
        print(str(puzzle[1])+" --> "+str(puzzle[0]))
        if(puzzle[0]==out):
          print("Solusi ditemukan")
          print('pada level ke-'+str(level))
          flag=True
          return
        else:
          level=level+1
          # up
          if(puzzle[1]!="down"):
            temp=copy.deepcopy(puzzle[0])
            up=move(temp, "up")
            if(up!=puzzle[0]):
              upx=[up,"up"]
              stack.insert(0, upx)
          # left
          if(puzzle[1]!="right"):
            temp=copy.deepcopy(puzzle[0])
            left=move(temp, "left")
            if(left!=puzzle[0]):
              leftx=[left,"left"]
              stack.insert(0, leftx)
          # down
          if(puzzle[1]!="up"):
            temp=copy.deepcopy(puzzle[0])
            down=move(temp, "down")
            if(down!=puzzle[0]):
              downx=[down,"down"]
              stack.insert(0, downx)
          # right
          if(puzzle[1]!="left"):
            temp=copy.deepcopy(puzzle[0])
            right=move(temp, "right")
            if(right!=puzzle[0]):
              rightx=[right,"right"]
              stack.insert(0, rightx)
```
`Iterative Deepening Search` (IDS) merupakan sebuah strategi umum yang biasanya dikombinasikan dengan Depth First tree search, yang akan menemukan berapa depth limit terbaik untuk digunakan. Hal ini dilakukan dengan secara menambah limit secara bertahap, mulai dari 0,1, 2, dan seterusnya sampai goal sudah ditemukan.
![enter image description here](https://image.slidesharecdn.com/iterativedeepeningsearch-141221081041-conversion-gate01/95/iterative-deepening-search-16-638.jpg?cb=1573413579)
Untuk Program tersebut saya mendapatkannya dari
Berikut ini adalah penjelasan dari tiap fungsi yang terdapat dalam  `IDS.py`:

1.  `move()`  : Fungsi ini digunakan untuk memindahkan angka di board sesuai dengan algoritma IDS.
2.  `ids()`  : Fungsi ini sebagai implementasi algoritma IDS dengan menggunakan stack, dan diperiksa tiap level hingga bertemu  `flag = true`.

### Heuristic 1 & 2
Source Code [8 Puzzle Heuristic](https://github.com/ohmyjons/Tugas-KB/blob/master/8Puzzle/Heuristic/heuristic-8puzzle.cpp)

Dalam program ini diminta untuk menyelesaikan 8 puzzle menggunakan metode heuristic 1 dan 2. Dimana penjelasan heuristic 1 dan 2 ada dibawah. Jika menggunakan heuristic 1 maka yang dilihat yaitu banyaknya grid yang menempati tempat yg salah, tetapi jika menggunakan heuristic 2 maka yang dilihat yaitu total keseluruhan jarak tiap grid yang menempati tempat yang salah terhadap posisi grid yang benar, atau sering disebut dengan manhattan distance.

Jadi dalam penyelesainnya kita mengeluarkan hasil setiap langkah puzzle dengan melihat penempatan grid yang salah kemudian dicari penempatan grid yang benar untuk mencapai final state yang diinginkan.

Program ini menggunakan tree, dengan kode sebagai berikut:
```
struct Node { 
	// stores the parent node of the current node helps in tracing path when the answer is found 
	Node* parent; 
	// stores matrix 
	int mat[N][N]; 
	// stores blank tile coordinates 
	int x, y; 
	// stores the number of misplaced tiles 
	int cost; 
	// stores the number of moves so far 
	int level; 
}; 
```

Kemudian setiap langkah pastinya memerlukan node untuk meletakkan grid nya, maka dari itu program dibawah ini untuk meyediakan node setiap langkah.
```
Node* newNode(int mat[N][N], int x, int y, int newX, int newY, int level, Node* parent) { 
	Node* node = new Node; 
	// set pointer for path to root 
	node->parent = parent; 
	// copy data from parent node to current node 
	memcpy(node->mat, mat, sizeof node->mat); 
	// move tile by 1 position 
	swap(node->mat[x][y], node->mat[newX][newY]); 
	// set number of misplaced tiles 
	node->cost = INT_MAX; 
	// set number of moves so far 
	node->level = level; 
	// update new blank tile cordinates 
	node->x = newX; 
	node->y = newY; 
	return node; 
} 
```

Karena heuristic ini melihat posisi grid yang salah, maka fungsi program dibawah ini untuk menghitung banyak nya angka yang tidak sesuai dengan final state.
```
int calculateCost(int initial[N][N], int final[N][N]) { 
	int count = 0; 
	for (int i = 0; i < N; i++) 
		for (int j = 0; j < N; j++) 
			if (initial[i][j] && initial[i][j] != final[i][j]) 
				count++; 
	return count; 
} 
```

Untuk bagian dibawah ini adalah pergerakan puzzle yang dimisalkan dengan `botton, left, top, right`
```
int row[] = { 1, 0, -1, 0 }; 
int col[] = { 0, -1, 0, 1 }; 
```

Setelah itu, fungsi dibawah ini untu megecek apakah posisi grid dimana angka didalamnya sudah sesuai dengan final statenya.
```
int isSafe(int x, int y) { 
	return (x >= 0 && x < N && y >= 0 && y < N); 
} 
```

Semua fungsi dijalankan dalam fungsi dibawah ini dimana untuk mengecek solusi penyelesaian menggunakan heuristic dengan initial awal puzzle yang dimasukkan kemudian final state yang diinginkan.
```
void solve(int initial[N][N], int x, int y, int final[N][N]) { 
	// Create a priority queue to store live nodes of search tree; 
	priority_queue<Node*, std::vector<Node*>, comp> pq; 
	// create a root node and calculate its cost 
	Node* root = newNode(initial, x, y, x, y, 0, NULL); 
	root->cost = calculateCost(initial, final); 
	// Add root to list of live nodes; 
	pq.push(root); 
	// Finds a live node with least cost, add its childrens to list of live nodes and 
	// finally deletes it from the list. 
	while (!pq.empty()) { 
		// Find a live node with least estimated cost 
		Node* min = pq.top(); 
		// The found node is deleted from the list of live nodes 
		pq.pop(); 
		// if min is an answer node 
		if (min->cost == 0) { 
			// print the path from root to destination; 
			printPath(min); 
			return; 
		} 
		// do for each child of min, max 4 children for a node 
		for (int i = 0; i < 4; i++) { 
			if (isSafe(min->x + row[i], min->y + col[i])) { 
				// create a child node and calculate its cost 
				Node* child = newNode(min->mat, min->x, 
							min->y, min->x + row[i], 
							min->y + col[i], 
							min->level + 1, min); 
				child->cost = calculateCost(child->mat, final); 

				// Add child to list of live nodes 
				pq.push(child); 
			} 
		} 
	} 
} 
```

Dalam bahasan ini, fungsi heuristik yang akan kita tampilkan yaitu adalah sebagai berikut.
- h₁(n) : sebagai banyak grid yang menempati tempat yang salah.
- h₂(n) : sebagai total keseluruhan jarak tiap grid yang menempati tempat yang salah terhadap posisi grid yang benar, atau sering disebut dengan manhattan distance.

Solusi Penyelesaian dengan fungsi Heuristik Pertama yaitu banyak grid yang menempati tempat yang salah

![8puzzle-heuristic1.1](https://user-images.githubusercontent.com/52326074/77029102-58f6c180-69cd-11ea-9571-7a69fe89de7d.PNG)
![8puzzle-heuristic1.2](https://user-images.githubusercontent.com/52326074/77029100-585e2b00-69cd-11ea-8d32-03512709f26c.PNG)
![8puzzle-heuristic1.3](https://user-images.githubusercontent.com/52326074/77029097-572cfe00-69cd-11ea-845e-7e8b50514214.PNG)

Solusi :
Initial State -> Right -> Up -> Right -> Down -> Down -> Left -> Up -> Right -> Down(Goal)

Solusi Penyelesai dengan fungsi Heuristik Kedua yaitu total keseluruhan jarak tiap grid yang menempati tempat yang salah terhadap posisi grid yang benar, atau sering disebut dengan manhattan distance.

![8puzzle-heuristic2.1](https://user-images.githubusercontent.com/52326074/77029181-8f344100-69cd-11ea-9799-24cda528fdd5.PNG)
![8puzzle-heuristic2.2](https://user-images.githubusercontent.com/52326074/77029178-8e9baa80-69cd-11ea-9d35-2282c1916e48.PNG)
![8puzzle-heuristic2.3](https://user-images.githubusercontent.com/52326074/77029175-8d6a7d80-69cd-11ea-8775-2fd302b4ad62.PNG)

Solusi :
Initial State -> Right -> Up -> Right -> Down -> Down -> Left -> Up -> Right -> Up(Goal)

-----	 
## 8 Queens

### BFS
8 Queens adalah permasalahan bagaimna bisa menempatkan 8 Ratu didalam kotak catur 8x8 dengan kondisi tidak ada salah satu dari Ratu tersebut yang saling menyerang, baik secara baris, kolom, maupun diagonal. Secara umum, 8 Queens ini adalah permasalahan N Queens dengan menempatkan N Ratu ke dalam NxN kotak catur.

![kondisi](https://github.com/prolifel/TugasKB_F/blob/master/Tugas/Assets/8q-bfs/Artboard%201-%204.jpg?raw=true)

  > _Source Code main.py:_ [main](https://github.com/prolifel/TugasKB_F/blob/master/Tugas/8%20Queens%20BFS/main.py)
  > _Source Code board.py:_ [board](https://github.com/prolifel/TugasKB_F/blob/master/Tugas/8%20Queens%20BFS/board.py)
  
  Berikut ini penjelasan mengenai setiap fungsi pada `board.py`:
  1. `__init__()` : Sebagai _constructor class_ `board` yang berisi `size` / ukuran dari board
  2. `solve_bfs()` : Digunakan sebagai implementasi dari algoritma BFS.
  3. `conflict()` : Digunakan apabila salah satu Ratu saling menyerang salah satu Ratu yang lain.
  4. `print()` : Digunakan sebagai _output_ board 8 Queens.
  
  Berdasarkan artikel [ini](https://doi.org/10.1145/185009.185019), dapat diketahui bahwa:
  > It is known that there are altogether 92 solutions. and one example is
  
  Hal ini sesuai dengan hasil program saya, yaitu:
  
  ![hasil_8q_bfs](https://github.com/prolifel/TugasKB_F/blob/master/Tugas/Assets/8q-bfs/Annotation%202020-04-12%20122128.png?raw=true)
  

#### Hill Climbing
  **Note**:
  Disini saya memakai kode Sabrina Jiang tanpa modifikasi. Kode tersebut bisa didapatkan [disini](https://github.com/Sabrina-Jiang/Hill-Climbing)
  
  Hill Climbing merupakan algoritma pencarian heuristik dengan optimisasi secara matematis. Disini, algoritma Hill Climbing tidak mencari solusi paling optimal, tetapi hanya mencari solusi yang masuk akal dari segi waktu. Pencarian heuristik adalah fungsi yang akan mengurutkan segala kemungkinan yang masuk akal dengan menggunakan _tree_ berdasarkan informasi yang ada. Hal tersebut membantu algoritma ini untuk memilih rute terbaik berdasarkan rute yang dapat dilalui.
  
  Berikut ini adalah ilustrasi dari algoritma Hill Climbing:
  
  ![HC](https://fileservice.slidewiki.org/media/images/25/4318.PNG)
  
  Dalam sebuah langkah-langkah sederhana, saya dapat mengartikan algoritma Hill Climbing sebagai berikut:
  1. Buat tree berdasarkan urutan random
  2. Tiap elemen pada array ditukar, kemudian dicari cost dari tiap kemungkinan
  3. Kemudian, _cost_ yang paling kecil dari cabang paling kiri, menjadi induk baru
  
  Dalam `hill_climbing.py` terdapat beberapa fungsi, yang terdiri dari:
  1. `get_num_of_conflict()` : Fungsi ini digunakan untuk menghitung konflik dari setiap Ratu dari kondisi papan catur sekarang yang kemudian menjadi _return value_ dari fungsi ini.
  2. `hill_climbing_first_choice()` : Fungsi ini sebagai implementasi dari langkah ketiga diatasm yaitu menemukan _cost_ yang paling kecil dari semua status yang ada.
  3. `prettyprint()` : Fungsi ini digunakan untuk print board. 'X' berarti Ratu dan '.' berarti tidak ada ratu.
  4. `Queens()` :  Fungsi digunakan sebagai prosedur utama dari algoritma Hill Climbing, yaitu menghitung konflik antar Ratu, dan jika konflik tersebut sama dengan nol, maka posisi/status Ratu tersebut sukses. Fungsi ini juga digunakan untuk menghitung _moving cost_ dari algoritma Hill Climbing, langkah yang akan diambil, dan waktu random start. Fungsi ini akan direkursif hingga dalam posisi/status sekarang sama dengan nol. _Return value_ dari fungsi ini adalah posisi/status sekarang.

-----
