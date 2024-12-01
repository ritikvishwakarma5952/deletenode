



public class Main
{
    static class Node{
        int data;
        Node right;
        Node left;
        
        Node(int data){
            this.data = data;
            right = null;
            left = null;
        }
    }
    
    public static void inorder(Node root){
        if(root == null){
            return;
        }
        
        inorder(root.left);
        System.out.print(root.data + " ");
        inorder(root.right);
    }
    
    public static Node insert(Node root, int data){
        if(root == null){
            return new Node(data);
        }
        
        if(data < root.data){
            root.left = insert(root.left, data);
        }else if(data > root.data){
            root.right = insert(root.right, data);
        }
        return root;
    }
    
    public static Node delete(Node root, int val){
	if (root == null) return root;

        if(root.data < val){
            root.right = delete(root.right, val);
        }else if(root.data > val){
            root.left = delete(root.left, val);
        }else{
            // case 1  - leaf node
            if(root.left == null && root.right == null){
                return null;
            }
            
            // case 2 - single child
            if(root.right == null){
                return root.left;
            }else if(root.left == null){
                return root.right;
            }
            
            // case 3 -- both child
            Node IS = findInorderSuccessor(root.right);
            root.data = IS.data;
            root.right = delete(root.right, IS.data);
        }
        return root;
    }
    
    public static Node findInorderSuccessor(Node root){
        while(root.left != null){
            root = root.left;
        }
        return root;
    }

	public static void main(String[] args) {
		int values[] = {8,5,3,1,4,6,10,11,14};
		Node root = null;
		
		for(int i=0; i<values.length; i++){
		    root = insert(root, values[i]);
		}
		
		inorder(root);
		System.out.println();
		
		root = delete(root,1);
		
		
		inorder(root);
		System.out.println();
}
}
