# DSA-Assignment
assignment
1.Given an array of elements, replace every element with nearest greater element on the right of that element.
Code: 
#include <iostream>
#include <set>
#include <vector>
using namespace std;
void solve (vector < int >&arr) {
   set < int >s;
   vector < int >ans (arr.size ());
   for (int i = arr.size () - 1; i >= 0; i--) {
      s.insert (arr[i]);
      auto it = s.upper_bound (arr[i]);
      if (it == s.end ())
         arr[i] = -1;
      else
         arr[i] = *it;
   }
}
void printArray (vector < int >&arr) {
   for (int i:arr)
      cout << i << " ";
   cout << "\n";
}
int main () {
   vector < int >arr = { 5, 23, 65, 31, 76, 32, 87, 23, 76, 32, 88 };
   printArray (arr);
   solve (arr);
   printArray (arr);
   return 0;
}

2.Recursively remove all adjacent duplicates: Given a string of characters, recursively
remove adjacent duplicate characters from the string. The output string should not have any adjacent duplicates.

Code: 
#include <bits/stdc++.h>
using namespace std;


char* removeUtil(char* str, char* last_removed)
{

	// If length of string is 1 or 0
	if (str[0] == '\0' || str[1] == '\0')
		return str;

	// Remove leftmost same characters and recur for
	// remaining string
	if (str[0] == str[1]) {
		*last_removed = str[0];
		while (str[1] && str[0] == str[1])
			str++;
		str++;
		return removeUtil(str, last_removed);
	}

	
	char* rem_str = removeUtil(str + 1, last_removed);

	
	if (rem_str[0] && rem_str[0] == str[0]) {
		*last_removed = str[0];

		// Remove first character
		return (rem_str + 1);
	}

	
	if (rem_str[0] == '\0' && *last_removed == str[0])
		return rem_str;

	
	rem_str--;
	rem_str[0] = str[0];
	return rem_str;
}

// Function to remove
char* remove(char* str)
{
	char last_removed = '\0';
	return removeUtil(str, &last_removed);
}

// Driver program to test above functions
int main()
{
	char str1[] = "Mississippi";
	cout << remove(str1) << endl;

	char str2[] = "deepak";
	cout << remove(str2) << endl;
	
	char str3[] = "careermonk";
	cout << remove(str3) << endl;
	
	return 0;
}

3.Given a list, List1={A1,A2,A3,……..An-1, An} with data, reorder it to {A1, An, A2, An1, …..} without using any extra space
Code:
#include <iostream>

using namespace std;

  class Node {
  public:
	int data;
	Node* next;
};


Node* newNode(int data)
{
	Node* new_node = new Node;
	new_node->data = data;
	new_node->next = NULL;
	return new_node;
}
 Node* reverse(Node* head)
    {
        Node* prev=NULL;
        Node* curr=head;
        Node* nxt=NULL;
        
        while(curr != NULL)
        {
            nxt=curr->next;
            curr->next=prev;
            prev=curr;
            curr=nxt;
        }
        return prev;
    }
    
    void reorderList(Node* head) {
        
        
        Node* slow=head;
        Node* fast=head->next;
        
        while(fast != NULL && fast->next != NULL)
        {
            slow=slow->next;
            fast=fast->next->next;
        }
        
       
        Node* second=reverse(slow->next); 
        slow->next=NULL;
        Node* first=head; 
        
        
        
        while(second != NULL)
        {
            Node* temp1=first->next;
            Node* temp2=second->next;
            first->next=second;
            second->next=temp1;
            first=temp1;
            second=temp2;
        }
    }
    void print(Node* head){
        Node* temp = head;
        while(temp != NULL){
            cout<<temp->data<<" ";
            temp = temp->next;
        }
        cout<<endl;
    }


int main()
{
    Node* head = newNode(1);
	head->next = newNode(2);
	head->next->next = newNode(3);
	head->next->next->next = newNode(4);
	head->next->next->next->next = newNode(5);
	print(head);
	reorderList(head);
	print(head);

    return 0;
}

4. Given a singly linked list, write a function to find root(n)th element, where n is the number of elements in the list. Assume value of n is not known in advance.
Code:
#include<stdio.h>
#include<stdlib.h>
 

struct Node
{
    int data;
    struct Node* next;
};
 

int printsqrtn(struct Node* head)
{
    struct Node* sqrtn = NULL;
    int i = 1, j = 1;
     
    
    while (head!=NULL)
    {  
        
        if (i == j*j)
        {  
            // for first node
            if (sqrtn == NULL)
                sqrtn = head;
            else
                sqrtn = sqrtn->next;
             
           
            j++;
        }
        i++;
         
        head=head->next;
    }
     
    
    return sqrtn->data;
}
 
void print(struct Node* head)
{
    while (head != NULL)
    {
        printf("%d ", head->data);
        head = head->next;
    }
    printf("\n");
}
 

void push(struct Node** head_ref, int new_data)
{
    // allocate node
    struct Node* new_node =
            (struct Node*) malloc(sizeof(struct Node));
     
    // put in the data
    new_node->data = new_data;
     
    // link the old list off the new node
    new_node->next = (*head_ref);
     
    // move the head to point to the new node
    (*head_ref) = new_node;
}
 
int main()
{
  
    struct Node* head = NULL;
    push(&head, 42);
    push(&head, 76);
     push(&head, 760);
      push(&head, 26);
      push(&head, 67); 
      push(&head, 97);
      push(&head, 77);
    push(&head, 200);
    push(&head, 10);
    printf("Given linked list is:");
    print(head);
    printf("sqrt(n)th node is %d ",printsqrtn(head));
     
    return 0;
}
5. [Find the modular node from the end:] Given a singly linked list, write a function to find the first from the end whose n%k==0, where n is the number of elements in the list and k is an integer constant. If n=19 and k=3 then we should return 16th node
Code:
#include<stdio.h>
#include<stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* newNode(int data)
{
    struct Node* new_node = malloc(sizeof(struct Node*));
    new_node->data = data;
    new_node->next = NULL;
    return new_node;
}
 

struct Node* modularNode(struct Node* head, int k)
{
   
    if (k <= 0 || head == NULL)
        return NULL;  
 
    
    int i = 1;
    struct Node* modularNode = NULL;
    for (struct Node* temp = head; temp != NULL; temp = temp->next) {
        if (i % k == 0)
            modularNode = temp;
         
        i++;
    }
    return modularNode;
}
 

int main(void)
{
    struct Node* head = newNode(1);
    head->next = newNode(2);
    head->next->next = newNode(3);
    head->next->next->next = newNode(4);
    head->next->next->next->next = newNode(5);
    int k = 3;
    struct Node* answer = modularNode(head, k);
    printf("\nModular node is ");
    if (answer != NULL)
        printf("%d\n", answer->data);
    else
        printf("null\n");
    return 0;
}
6. Given an array of n numbers, create an algorithm which displays all pairs whose sum is S.
Code:
#include <iostream>
#include <algorithm>//#include <bits/stdc++.h>

using namespace std;
 
void pairedElements(int arr[], int sum, int n)
{
    int low = 0;
    int high = n - 1;
 
    while (low < high) {
        if (arr[low] + arr[high] == sum) {
            cout << "The pair is : (" << arr[low] << ", "
                 << arr[high] << ")" << endl;
        }
        if (arr[low] + arr[high] > sum) {
            high--;
        }
        else {
            low++;
        }
    }
}
 
// Driver code
int main()
{
    int arr[] = { 2, 3, 4, -2, 6, 8, 9, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);
    sort(arr, arr + n);
    pairedElements(arr, 6, n);
}
7. If h is an hashing function and is used to hash n keys into a table of size s, where n<=s, the expected number of collisions involving a particular key X is.
Code:
#include <iostream>

double expected_collisions(int n, int s) {
    return (double)(n - 1) / s;
}

int main() {
    int n = 10; // number of keys
    int s = 15; // table size
    int x = 3;  // particular key
    double expected = expected_collisions(n, s);
    std::cout << "Expected number of collisions for key " << x << " is " << expected << std::endl;
    return 0;
}
8. [Josephus circle:] N people decided to elect a leader by arranging themselves in a circle and eliminating every mth person around the circle, closing ranks as each drops out. Find which person will be the last one remaining (with rank 1).
Code:
#include <bits/stdc++.h>

using namespace std;

void Josh(vector<int> person, int k, int index)
{
	
	if (person.size() == 1) {
		cout << person[0] << endl;
		return;
	}

	index = ((index + k) % person.size());

	
	person.erase(person.begin() + index);

	Josh(person, k, index);
}

int main()
{
	int n = 14; 
				
	int k = 2;
	k--; 
	int index =0;
		

	vector<int> person;
	// fill the person vector
	for (int i = 1; i <= n; i++) {
		person.push_back(i);
	}

	Josh(person, k, index);
}
9. For a given k value (k>0) reverse blocks of nodes in the list. Example: Input: 1,2,3,4,5,6,7,8,9,10 Output for different k values: For k=2: 2,1,4,3,6,5,8,7,10,9 For k=3: 3,2,1,6,5,4,9,8,7,10 For k=4: 4,3,2,1,8,7,6,5,9,10
Code:
#include <stdio.h>
#include <stdlib.h>

struct Node
{
	int data;
	struct Node* next;
};


void printList(struct Node* head)
{
	struct Node* ptr = head;
	while (ptr)
	{
		printf("%d —> ", ptr->data);
		ptr = ptr->next;
	}

	printf("NULL\n");
}


void push(struct Node** head, int data)
{
	struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
	newNode->data = data;
	newNode->next = *head;

	*head = newNode;
}


struct Node* reverseK(struct Node** current, int k)
{
	struct Node* prev = NULL;
	int count = 0;

	
	while (*current && count++ < k)
	{
		
		struct Node* next = (*current)->next;

		(*current)->next = prev;

		prev = *current;

		*current = next;
	}


	return prev;
}


void reverseInGroups(struct Node **head, int k)
{
	
	if (*head == NULL) {
		return;
	}

	struct Node* current = *head;

	
	struct Node* prev = reverseK(&current, k);

	
	reverseInGroups(&current, k);

	(*head)->next = current;
	*head = prev;
}

int main(void)
{
	// input keys
	int keys[] = { 1, 2, 3, 4, 5, 6, 7, 8 };
	int n = sizeof(keys)/sizeof(keys[0]);

	struct Node* head = NULL;
	for (int i = n - 1; i >=0; i--) {
		push(&head, keys[i]);
	}

	reverseInGroups(&head, 3);

	printList(head);

	return 0;
}
10. Suppose there are two singly linked lists both of which intersect at some point and become a singly list. The head or starting pointers for the both lists are known, but the intersecting node is not known. Also the number of nodes in each of the lists before they intersect is unknown and may be different in each list. List1 may have n nodes before it reaches the intersection point, and list2 might have m nodes before it reaches the intersection point where m and n may be m=n, mn. write a program for find a merging node.
Code:
#include <bits/stdc++.h>
using namespace std;

class Node {
public:
	int data;
	Node* next;
};


int getCount(Node* head);

/
int _getIntesectionNode(int d, Node* head1, Node* head2);



int getIntesectionNode(Node* head1, Node* head2)
{

	// Count the number of nodes in
	// both the linked list
	int c1 = getCount(head1);
	int c2 = getCount(head2);
	int d;

	// If first is greater
	if (c1 > c2) {
		d = c1 - c2;
		return _getIntesectionNode(d, head1, head2);
	}
	else {
		d = c2 - c1;
		return _getIntesectionNode(d, head2, head1);
	}
}


int _getIntesectionNode(int d, Node* head1, Node* head2)
{
	// Stand at the starting of the bigger list
	Node* current1 = head1;
	Node* current2 = head2;

	// Move the pointer forward
	for (int i = 0; i < d; i++) {
		if (current1 == NULL) {
			return -1;
		}
		current1 = current1->next;
	}

	// Move both pointers of both list till they
	// intersect with each other
	while (current1 != NULL && current2 != NULL) {
		if (current1 == current2)
			return current1->data;

		// Move both the pointers forward
		current1 = current1->next;
		current2 = current2->next;
	}

	return -1;
}


int getCount(Node* head)
{
	Node* current = head;

	// Counter to store count of nodes
	int count = 0;

	// Iterate till NULL
	while (current != NULL) {

		// Increase the counter
		count++;

		// Move the Node ahead
		current = current->next;
	}

	return count;
}


int main()
{
	/*
		Create two linked lists
	
		1st 3->6->9->15->30
		2nd 10->15->30
	
		15 is the intersection point
	*/

	Node* newNode;

	// Addition of new nodes
	Node* head1 = new Node();
	head1->data = 10;

	Node* head2 = new Node();
	head2->data = 3;

	newNode = new Node();
	newNode->data = 6;
	head2->next = newNode;

	newNode = new Node();
	newNode->data = 9;
	head2->next->next = newNode;

	newNode = new Node();
	newNode->data = 15;
	head1->next = newNode;
	head2->next->next->next = newNode;

	newNode = new Node();
	newNode->data = 30;
	head1->next->next = newNode;

	head1->next->next->next = NULL;

	cout << "The node of intersection is " << getIntesectionNode(head1, head2);
}
11. Check whether the given linked list is either NULL-terminated or ends in cycle (cyclic).
Code:
#include <stdio.h>
#include <stdlib.h>

struct Node {
 int data;
 struct Node* next;
};

void push(struct Node** head_ref, int new_data)
{

 struct Node* new_node
  = (struct Node*)malloc(sizeof(struct Node));


 new_node->data = new_data;

 new_node->next = (*head_ref);

 (*head_ref) = new_node;
}

int detectLoop(struct Node* list)
{
 struct Node *slow_p = list, *fast_p = list;

 while (slow_p && fast_p && fast_p->next) {
  slow_p = slow_p->next;
  fast_p = fast_p->next->next;
  if (slow_p == fast_p) {
   return 1;
  }
 }
 return 0;
}

int main()
{

 struct Node* head = NULL;

 push(&head, 20);
 push(&head, 4);
 push(&head, 15);
 push(&head, 10);


 head->next->next->next->next = head;

 if (detectLoop(head))
  printf("Loop Found");
 else
  printf("No Loop");
 return 0;
}
12. Given an array of characters formed with a’s and b’s. The string is marked with special character X which represents the middle of the list (for example: ababa…ababXbabab….baaaa). Check whether the string is palindrome.
Code:
#include<iostream>
#include<string>
using namespace std;

int isPalindrome(char *str, int n)
{

 int start_index = 0;
 

 int last_index = n-1;
 
 while(start_index < last_index && str[start_index] == str[last_index])
 {
  
  start_index++;
  last_index--;
 }
 
 if(start_index < last_index)
 {
  
  cout<<"NOT A PALINDROME"<<endl;
  return 0;
 }
 else
 {
  //we reached the center
  cout<<"PALINDROME"<<endl;
  return 1;
 }
}

int main(void)
{
 char *s1 = "abaXaba";
 
 char *s2 = "aaabbbXbbbaaa";

 
 char *s3 = "abababababbabXbababbbbabba";
 
 int x;
 x = isPalindrome(s1,7);
 x = isPalindrome(s2,13);
 x = isPalindrome(s3,27);
 return 0;
}
13. How do we implement two stacks using only one array? Our stack routines should not indicate an exception unless every slot in the array is used.
Code:
#include <stdio.h>  
#define SIZE 20  
 int array[SIZE];   
int top1 = -1;  
int top2 = SIZE;  
   
  
void push1 (int data)  
{  

  if (top1 < top2 - 1)  
  {  
      top1++;  
    array[top1] = data;  
  }  
  else  
  {  
    printf ("Stack is full");  
  }  
}  

void push2 (int data)  
{  
    
if (top1 < top2 - 1)  
  {  
    top2--;  
    array[top2] = data;   
  }  
  else  
  {  
    printf ("Stack is full..\n");  
  }  
}  
   

void pop1 ()  
{  
 
 if (top1 >= 0)  
  {  
    int popped_element = array[top1];  
    top1--;  
     
    printf ("%d is being popped from Stack 1\n", popped_element);  
  }  
  else  
  {  
    printf ("Stack is Empty \n");  
  }  
}  
 
void pop2 ()  
{  
    
if (top2 < SIZE)  
  {  
      int popped_element = array[top2];  
    top2--;  
     
    printf ("%d is being popped from Stack 1\n", popped_element);  
  }  
  else  
  {  
    printf ("Stack is Empty!\n");  
  }  
}  
   
  
void display_stack1 ()  
{  
  int i;  
  for (i = top1; i >= 0; --i)  
  {  
    printf ("%d ", array[i]);  
  }  
  printf ("\n");  
}  

void display_stack2 ()  
{  
  int i;  
  for (i = top2; i < SIZE; ++i)  
  {  
    printf ("%d ", array[i]);  
  }  
  printf ("\n");  
}  
   
int main()  
{  
  int ar[SIZE];  
  int i;  
  int num_of_ele;  
   
  printf ("We can push a total of 20 values\n");  
   
  //Number of elements pushed in stack 1 is 10  
  //Number of elements pushed in stack 2 is 10  
   
// loop to insert the elements into Stack1    
for (i = 1; i <= 10; ++i)  
  {  
    push1(i);  
    printf ("Value Pushed in Stack 1 is %d\n", i);  
  }  
// loop to insert the elements into Stack2.    
for (i = 11; i <= 20; ++i)  
  {  
    push2(i);  
    printf ("Value Pushed in Stack 2 is %d\n", i);  
  }  
   
  //Print Both Stacks  
  display_stack1 ();  
 display_stack2 ();  
   
  
  printf ("Pushing Value in Stack 1 is %d\n", 11);  
  push1 (11);  
   
   
  num_of_ele = top1 + 1;  
  while (num_of_ele)  
  {  
    pop1 ();  
    --num_of_ele;  
  }  
   
  
  pop1 ();  
   
  return 0;  
}  
14. Show how to implement one queue efficiently using two stacks. Analyse the running time of queue operations
Code:
#include <bits/stdc++.h>
using namespace std;

struct Queue {
	stack<int> s1, s2;

	void enQueue(int x)
	{
		
		while (!s1.empty()) {
			s2.push(s1.top());
			s1.pop();
		}

		
		s1.push(x);

		while (!s2.empty()) {
			s1.push(s2.top());
			s2.pop();
		}
	}

	int deQueue()
	{
		// if first stack is empty
		if (s1.empty()) {
			cout << "Q is Empty";
			exit(0);
		}

		// Return top of s1
		int x = s1.top();
		s1.pop();
		return x;
	}
};

// Driver code
int main()
{
	Queue q;
	q.enQueue(54);
	q.enQueue(46);
	q.enQueue(4);

	cout << q.deQueue() << '\n';
	cout << q.deQueue() << '\n';
	cout << q.deQueue() << '\n';

	return 0;
}
15. Show how to implement one stack efficiently using two queues. Analyse the running time of stack operations.
Code:
#include <bits/stdc++.h>

using namespace std;

class Stack {
	
	queue<int> q1, q2;

public:
	void push(int x)
	{
		
		q2.push(x);

		while (!q1.empty()) {
			q2.push(q1.front());
			q1.pop();
		}

		
		queue<int> q = q1;
		q1 = q2;
		q2 = q;
	}

	void pop()
	{
		
		if (q1.empty())
			return;
		q1.pop();
	}

	int top()
	{
		if (q1.empty())
			return -1;
		return q1.front();
	}

	int size() { return q1.size(); }
};


int main()
{
	Stack s;
	s.push(5);
	s.push(6);
	s.push(3);

	cout << "current size: " << s.size() << endl;
	cout << s.top() << endl;
	s.pop();
	cout << s.top() << endl;
	s.pop();
	cout << s.top() << endl;

	cout << "current size: " << s.size() << endl;
	return 0;
}
16. Given a stack of integers, how do you check whether each successive pair of members in the stack is consecutive or not. The pairs can be increasing or decreasing, and if the stack has an odd number of elements, the element at the top is left out of pair. For example, if stack of elements are [4, 5, -2, -3, 11, 10, 5, 6, 20], then the output should be true because each of the pairs (4,5), (-2,-3), (11,10) and (5,6) consists of consecutive numbers.
Code:
#include <bits/stdc++.h>
using namespace std;


bool pairWiseConsecutive(stack<int> s)
{
	
	stack<int> aux;
	while (!s.empty()) {
		aux.push(s.top());
		s.pop();
	}

	
	bool result = true;
	while (aux.size() > 1) {

		
		int x = aux.top();
		aux.pop();
		int y = aux.top();
		aux.pop();
		if (abs(x - y) != 1)
		result = false;
}	

return result;
}
int main()
{
	stack<int> s;
	s.push(4);
	s.push(5);
	s.push(-2);
	s.push(-3);
	s.push(11);
	s.push(10);
	s.push(5);
	s.push(6);
	s.push(20);

	if (pairWiseConsecutive(s))
		cout << "Yes" << endl;
	else
		cout << "No" << endl;
	return 0;
}
17. Given array[] with sliding window of size w which is moving from the very left of the array to very right. Assume that we can only see the w numbers in the window. Each time the sliding window moves right forwards by on position. For example: The array is [1 3 -1 -3 5 3 6 7], and w is 3. Window position Max [1 3 -1] -3 5 3 6 7 3 1 [3 -1 -3] 5 3 6 7 3 1 3 [-1 -3 5] 3 6 7 5 1 3 -1 -3 [5 3 6] 7 5 1 3 -1 -3 5 [3 6 7] 6 1 3 -1 -3 5 3 6 7 7
Code:
#include <stdio.h>
#include <iostream>
using namespace std;

void printKMax(int arr[], int N, int K)
{
	int j, max;

	for (int i = 0; i <= N - K; i++) {
		max = arr[i];

		for (j = 1; j < K; j++) {
			if (arr[i + j] > max)
				max = arr[i + j];
		}
		printf("%d ", max);
	}
}


int main()
{
	int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
	int N = sizeof(arr) / sizeof(arr[0]);
	int K = 3;

	// Function call
	printKMax(arr, N, K);	
	return 0;
}
19. Given an integer k and a queue of integers, how do you reverse the order of first k elements of the queue, leaving the other elements in the same relative order? For example, if k=4 and queue have the elements [10, 20, 30, 40, 50, 60, 70, 80, 90]; the output should be [40, 30, 20, 10, 50, 60, 70, 80, 90].
Code:
#include<iostream>
#include<queue>
#include<stack>
using namespace std;


void reverseQueueFirstKElements(int k, queue<int>& Queue)
{
	if (Queue.empty() == true || k > Queue.size())
		return;
	if (k <= 0)
		return;

	stack<int> Stack;

	
	for (int i = 0; i < k; i++) {
		Stack.push(Queue.front());
		Queue.pop();
	}

	
	while (!Stack.empty()) {
		Queue.push(Stack.top());
		Stack.pop();
	}

	
	for (int i = 0; i < Queue.size() - k; i++) {
		Queue.push(Queue.front());
		Queue.pop();
	}
}


void Print(queue<int>& Queue)
{
	while (!Queue.empty()) {
		cout << Queue.front() << " ";
		Queue.pop();
	}
}

int main()
{
	queue<int> Queue;
	Queue.push(10);
	Queue.push(20);
	Queue.push(30);
	Queue.push(40);
	Queue.push(50);
	Queue.push(60);
	Queue.push(70);
	Queue.push(80);
	Queue.push(90);

	int k = 4;
	reverseQueueFirstKElements(k, Queue);
	Print(Queue);
}

