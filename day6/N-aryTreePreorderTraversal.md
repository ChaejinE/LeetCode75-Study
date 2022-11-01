# Intro
- Preorder, Stack, 깊이탐색

# Solution
- list input을 주고, 해당 노드를 전위 순회하는 순서의 값을 vector로 Return 한다.

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
public:
    vector<int> preorder(Node* root) {
        vector<int> result;
        
        if (!root)
            return result;
            
        stack<Node*> stk;
        unordered_map<Node*, bool> visited;
        
        stk.push(root);
        visited[root] = true;
        Node* currentNode;
        vector<Node*> currentChildren;
        while (!stk.empty()) {
            currentNode = stk.top();
            result.emplace_back(currentNode->val);
            currentChildren = currentNode->children;
            stk.pop();
            
            for (int i = (currentChildren.size() - 1); i >= 0; --i) {
                if (visited.find(currentChildren[i]) == visited.end()) {
                    stk.push(currentChildren[i]);
                    visited[currentChildren[i]] = true;
                }
            }
        }
        
        return result;
    }
};
```
- 깊이 우선 탐색이 필요한 것으로 파악했다.

![image](https://user-images.githubusercontent.com/69780812/199235570-894d6dc0-411d-459e-87af-91135c365fc2.png)
- 반복문으로 구현한 이유는 이같은 문장을 봐서 ? 이다. 깊이가 1000인데, recursive로 구현해되 될듯한데 왜일지는 모르겠다. 그래도 경험쌓을겸 iterative하게 구현했다.

- 왼쪽 자식 노드부터 깊이탐색을 하기위해, reverse로 stack에 push 했다.
- 이후 dfs와 마찬가지로 visited로 방문을 처리했다.
  - 일단 visited처럼 ```vector<bool>```로 하지 않은 이유는 val 값이 겹치는 Exception이 발생했기 때문이다. 즉, val을 인덱스로하는 visted를 만들 수 없어 그냥 hash map으로 대체했다.
- 이후 stack 자료형의 특성으로 왼쪽 자식 노드부터 전위순회하는 결과를 담아 return 할 수 있었다.

## The Other Solution
```cpp
class Solution {
public:
    void solve(Node* root, vector<int> &ans){
        ans.emplace_back(root->val);
        for(int i = 0;i<root->children.size();i++){
            solve(root->children[i],ans);
        }
    }
    vector<int> preorder(Node* root) {
        vector<int> ans;
        if(!root) return ans;
        solve(root,ans);
        return ans;
    }
};
```
- 이게 완벽한거 같다.
- 역시 Recursive가 가능하다.
