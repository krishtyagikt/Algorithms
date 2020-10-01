# Algorithms

## Graph Algorithms

1. DFS

```c++
#include<bits/stdc++.h>
using namespace std;

# define C continue;
# define R return

# define D double
# define I insert
# define ll long long
# define ld long double

# define ull unsigned long long
# define ui unsigned int

# define pb push_back
# define pf push_front

# define vi vector < int >
# define vc vector < char >
# define vs vector < string >
# define vb vector < bool >
# define vd vector < D >
# define vll vector < ll >
# define vull vector < ull >
# define vld vector < ld >
# define PQ priority_queue

# define vvi vector < vector < int > >
# define vvb vector < vector < bool > >
# define vvc vector < vector < char > >
# define vvs vector < vs >
# define vvll vector < vector < ll > >
# define vvd vector < vector < D > >
# define vvld vector < vector < ld > >

# define all(v) (v).begin() , (v).end()
# define allrev(v) (v).rbegin() , (v).rend()
# define allcomp(v) v.begin() , v.end() , comp
# define allrevcomp(v) v.rbegin() , v.rend() , comp

# define pii pair < int , int >
# define pll pair < ll , ll >
# define pld pair < ld , ld >
# define pDD pair < D , D >

# define vpld vector < pld >
# define vpii vector < pii >
# define vpll vector < pll >
# define vpDD vector < pDD >

# define vvpii vector < vector < pii > >
# define F first
# define S second
# define mp make_pair

# define dist(a,b,p,q) sqrt((p-a)*(p-a) + (q-b)*(q-b))

# define pp(n) printf("%.10Lf",n);
# define line cout<<"\n";
# define fast ios_base::sync_with_stdio(false) ; cin.tie(0) ; cout.tie(0);

string vow = "aeiou";
int month[] = {-1, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

const int dxhorse[] = {-2, -2, -1, -1, 1, 1, 2, 2};
const int dyhorse[] = {1, -1, 2, -2, 2, -2, 1, -1};

const int dx[] = { -1 , 0 , 1 , 0 } ;
const int dy[] = { 0 , 1 , 0 , -1 } ;

const ld pie = 3.1415926535897932384626 ;
const ll mod = 1e9 + 7 ;

/// Tip : If a and b are positive integers ; we may say - ceil (a/b) = 1 + floor ( (a-1)/b ) .

/// ------------------------------------------------------------------------------------------------

/// This is the basic code of dfs ; which will give dfs order ; for an undirected graph ; having 'n' vertices ; and 'm' edges
/// Note - The dfs order is not unique for a graph

const int N = 10; /// this is the max number of vertices for any graph ( depends on constraints of problem )

vi g[N] ;
int n , m ;

void read ()
{
    cin >> n >> m ;

    for ( int i=0 ; i < m ; i ++ ) /// for m edges that will be input
    {
        int a , b ;
        cin >> a >> b ;
        
        /// question says that there is an undirected edge a-b in the graph
        /// an undirected edge a-b can be understood as two directed edges - a to b and other : b to a

        g[a].pb ( b ) ; /// This serves for directed edge a to b
        g[b].pb ( a ) ; /// This serves for directed edge b to a
        
        /// Had this been a directed graph ; we would only have done - g[a].pb ( b ) ; 
        
    }
}

bool vis[N] ;

void dfs ( int node )
{
    vis[node] = 1 ;

    cout << node << " " ; /// Prints the dfs order

    for ( auto &i : g[node] )
    {
        if ( vis[i] ) C ; /// don't go on some already visited vertex ; 
        /// else you would be stuck in an infinite loop a to b , b to a , a to b ... infinite times
        
        dfs ( i ) ; /// go to a non visited node
    }
}

void solve ( int test_case )
{
    read ();

    int start ; /// the node from which we will start dfs
    cin >> start ;

    dfs ( start ) ;
    
    /// NOTE : on changing this start node ; the dfs order on the same graph will change
}

int main()
{
    int t = 1;
    // cin >> t;

    for ( int i=1 ; i <= t ; i ++ ) solve ( i ) ;
    return 0;
}

```


2. Bipartite Graph Test

```c++

#include<bits/stdc++.h>
 
using namespace std ;
 
typedef double D ;
typedef long long ll ;
typedef long double ld ;
typedef unsigned int ui ;
typedef unsigned long long ull ;
 
# define F first
# define S second
# define R return
# define C continue 
# define pb push_back 
# define pf push_front
# define mp make_pair
 
# define vi vector <int>
# define vb vector <bool>
# define vll vector <ll>
# define vs vector <string>
 
# define vvi vector < vector < int > >
# define vvb vector < vector < bool > >
# define vvc vector < vector < char > >
# define vvll vector < vector < ll > >
# define vvd vector < vector < D > >
# define vvld vector < vector < ld > >
 
# define pii pair < int , int >
# define pll pair < ll , ll >
# define pld pair < ld , ld >
# define pDD pair < D , D >
 
# define vpld vector < pld >
# define vpii vector < pii >
# define vpll vector < pll >
# define vpDD vector < pDD >
# define vvpii vector < vector < pii > >
 
# define all(v) (v).begin() , (v).end()
# define allrev(v) (v).rbegin() , (v).rend()
# define allcomp(v) v.begin() , v.end() , comp
# define allrevcomp(v) v.rbegin() , v.rend() , comp

# define dist(a,b,p,q) sqrt((p-a)*(p-a) + (q-b)*(q-b))

# define FAST ios_base :: sync_with_stdio (false) ; cin.tie(0) ; cout.tie(0)
 
const ll MOD = 1e9 + 7 ;
const int infi =  INT_MAX ;
const ll infll =  LLONG_MAX ;
const ld PI = 3.1415926535897932384626 ;
 
///////////////////////////////////////////////////////////////////////////////////////

void bad(){
	cout << -1 << '\n' ;
	exit (0) ;
}

const int N = 1e5 + 10 ;

int n , m , u , v ;
vi adj [N] ;
vi col (N) ;

void read(){ // reading the graph ;
	cin >> n >> m ;
	for (int i = 0 ; i < m ; ++i){
		int u , v ;
		cin >> u >> v ;
		--u ;
		--v ;
		adj[u].pb(v) ;
		adj[v].pb(u) ;
	}
}

void dfs(int node){
	for (int &child : adj[node]){
		if (col[child] == col[node]){
			bad() ;
		}
		if (col[child] == 0){
			col[child] = 3 - col[node] ; // color will be either 1 or 2 (bipartite condition) ;
			dfs(child) ;
		}
	}
}

void solve (int test_case){
	read() ;
	for (int i = 0 ; i < n ; ++i){ // why loop ? coz a graph can have unconncted components (we assume) ;
		if (col[i] == 0){
			col[i] = 1 ;
			dfs(i) ;
		}
	}
	int cnt = 0 ;
	for (int i = 0 ; i < n ; ++i){
		if (col[i] == 1){
			++cnt ;
		}
	}
	cout << cnt << '\n' ; // count of nodes with color = 1 ;
	for (int i = 0 ; i < n ; ++i){
		if (col[i] == 1){
			cout << i+1 << ' ' ; // node value with color = 1 ;
		}
	}
	cout << '\n' ;
	cout << n - cnt << '\n' ; // count of nodes with color = 2 ;
	for (int i = 0 ; i < n ; ++i){
		if (col[i] == 2){
			cout << i+1 << ' ' ; // node value with color = 2 ;
		}
	}
	cout << '\n' ;
}
 
int main(){
	//freopen ("input.txt","r",stdin) ;
	//freopen ("output.txt","w",stdout) ;
	FAST ;
	int tc = 1 ;
//	cin >> tc ;
	while (tc--){
		solve (tc) ;
	}
	return 0 ;
}


```
