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
 
int rec(int init, int sum,vector<int>& dp)  {
  if(init > sum) {
    return 0;
  }
  if(init == sum) {
    return 1;
  }
  if(dp[init] != -1) {
    return dp[init];
  } 
  int ans = 0;
  for(int i = 1; i<=6;i++) {
       if(i > sum) {
         continue;
       }
      ans += rec(init + i,sum,dp);
  }
  return dp[init] = ans % 1000000007;
}
 
void solve()
{
  int n;
  cin >> n;
  vector<int> dp(n,-1);
  cout << rec(0,n,dp) % 1000000007 << endl;
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
  // }
   

```
