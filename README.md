#include<bits/stdc++.h>
#define ll long long 
#define ul unsigned long 
#define ull unsigned long long 
#define MOD 1000000007
const int N = 1e5 + 5;

#define p(a,b) pair<a,b>
#define ff first
#define ss second
#define pb push_back

#define for1(i,a,b) for(int i = a;i<b;++i)
#define for2(i,b) for(int i = b;i>=0;--i) 

// it has only veriabe tp always veriable.
#define vec1(tp,sz,ini) vector<tp> v1(sz,ini); 
#define vec2(tp,sz,ini) vector<tp> v2(sz,ini);
#define vec2D(tp,sz,ini)vector<vector<tp>> vD(sz,vector<int>(sz,ini));

#define ci  cin>> 
#define co  cout<< 
#define e   '\n'

#define deb1(x) cout<<#x<<" : "<<x<<endl;
#define deb2(x,y) cout<<#x<<" : "<<x<<" "<<#y<<" : "<<y<<endl;
#define deb3(x,y,z) cout<<#x<<" : "<<x<<"   "<<#y<<" : "<<y<<"  "<<#z<<" : "<<z<<endl;

#define FAST ios_base::sync_with_stdio(false),cin.tie(0),cout.tie(0);
#define READ freopen("input.txt","r",stdin);
#define WRITE freopen("output.txt","w",stdout);
#define RANDOM srand(time(NULL));

using namespace std;
const bool testCase = 0;
#define M 4
#define N 4

struct Que {
	Que(int x, int y, int dist) {
		this->x = x;
		this->y = y;
		this->dist = dist;
	}
	int x, y, dist,la;
};
class cmp {
public:
	bool operator()(Que a, Que b) {
		if (a.la == b.la) {
			return a.dist > b.dist;
		}
		else {
			return a.la < b.la;
		}
	}
};
priority_queue<Que,vector<Que>, cmp> pq;

void minDistance(vector<vector<int>> grid,int r,int c) {

	Que source(0, 0, 0);
	vector<vector<bool>> visited(r, vector<bool>(c));
	/*for1(i, 0, N) {
		for1(j, 0, M) {
			if (grid[i][j] == '0') {
				visited[i][j] = true;
			}
			else visited[i][j] = false;

			if (grid[i][j] == 's')
			{
				source.x = i;
				source.y = j;
			}
		}
	}*/

	queue<Que> q;

	q.push(source);
	visited[0][0] = true;
	while (!q.empty()) {
		Que ob = q.front();
		q.pop();

		//if (grid[ob.x][ob.y] == 'd')
			//return ob.dist;
		int x[8] = { -1,0,1,0,-1,-1,1,1 };
		int y[8] = { 0,1,0,-1,-1,1 ,1,-1};
		int ct = 0;
		for1(i, 0, 8) {
			int rc = ob.x + x[i];
			int cc = ob.y + y[i];
			if (rc < 0 || rc >= r) continue;
			if (cc < 0 || cc >= c) continue;
			if (grid[rc][cc] != 0) ct++;
		    
			if (!visited[rc][cc]) 
			{
				
				q.push(Que(rc, cc, ob.dist + 1));

				visited[rc][cc] = true;
			}


		}

		if (!(ob.x == 0 && ob.y ==0) && grid[ob.x][ob.y] != 0) {
			ob.la = ct;
			pq.push(ob);
		}

	}
	



}

int main() {

	FAST

		ll t = 1;
	if (testCase) {
		cin >> t;
	}
	while (t-- > 0)
	{

		ll r, c;
		cin >> r >> c;
		int temp;
		vector<vector<int>> grid(r, vector<int>(c,0));
		for1(i,0,r) {
			for1(j,0,c) {
				cin >> grid[i][j];
			}
		}

		minDistance(grid,r,c);
		Que ob= pq.top();
		cout << ob.x+1 << " : " << ob.y+1 << " : " << ob.la << e;













	}


	return 0;
}




