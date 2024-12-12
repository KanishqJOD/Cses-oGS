```cpp
////////////
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ll long long
#define inp(v) for(auto &it: v) cin>>it
#define pyes cout <<"YES\n";
#define pno cout <<"NO\n";
#define pb push_back
#define pii pair<int,int>
#define vi vector<int>
#define vll vector<long long>
#define all(x) x.begin(),x.end()
#define INF INT_MAX
#define MOD 1000000007
// log2(A)==Highest set bit in
int get_msb(int a) {if (a == 0) return -1;int msb = 0;while (a > 1) {a >>= 1;msb++;}return msb;}
 
// prime genrator
 
vector<int> primes_(int n) {vector<bool> sieve(n+1, true);vector<int> primes;for (int p = 2; p <= sqrt(n); ++p) {if (sieve[p]) {for (int i = p*p; i <= n; i += p)  sieve[i] = false;}}for (int p = 2; p <= n; ++p) {if (sieve[p])primes.push_back(p);}return primes;}
// lcm
inline int lcm(int a ,int b){return a*b/__gcd(a,b);}
//calculate lcm of entire vector
int lcm_v(vector<int>&v){int ans=1;for (auto & it : v){ans=lcm(ans,it);}return ans;}
//prints vector
void print_vec(vector<int>&v){for (auto & it : v){cout <<it<<" ";}}
 


// int rec(int index, int target, vector<vector<int>> &dp, vector<int> &arr) {
//     if (target == 0) return 0;
//     if (index == 0) {
//         if (target % arr[0] == 0) return target / arr[0]; 
//         else return INF; 
//     }
//     if (dp[index][target] != -1) return dp[index][target]; 
    
//     int notPick = rec(index - 1, target, dp, arr); 
//     int pick = INF;
//     if (arr[index] <= target) {
//         pick = 1 + rec(index, target - arr[index], dp, arr);
//     }
//     return dp[index][target] = min(pick, notPick);
// }


void solve() {
    ll n, x;
    cin >> n >> x;
    vector<int> c(n);
    for (int i = 0; i < n; i++) cin >> c[i];
    
    vector<int> curr(x + 1, INT_MAX), prev(x + 1, INT_MAX);
    
    curr[0] = 0;

    for (int index = 0; index < n; index++) {
        for (int target = 0; target <= x; target++) {
            int notPick = curr[target]; 
            int pick = INT_MAX;

            if (c[index] <= target && curr[target - c[index]] != INT_MAX) {
                pick = 1 + curr[target - c[index]];  
            }

            curr[target] = min(pick, notPick); 
        }

    }

    int result = curr[x];  
    if (result == INT_MAX) {
        cout << -1 << endl; 
    } 
    else {
        cout << result << endl;  
    }
}







signed main()
{
    // kanishq
    // Tahalyani
   ios_base::sync_with_stdio(false);
   cin.tie(NULL); cout.tie(NULL);
  // int t;
  // cin >> t;
  // while (t--)
  // {
   solve();
 //  }
   
}
```
