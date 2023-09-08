# BehaviourTree-Unity
Basic implementation of a behavior tree in C# adapted to Unity. Feel free to use it for any project and/or purpose.

## How to use

Note: Import BehaviourTree package to use auxiliar classes.

### 1. Create some action nodes

For this porpose you just need create a class that inherite from Node class.
Override Evaluate method where you can set the behaviour of that node and return 
the NodeState value acordingly.

Also you can create a customized constructor to keep track of relevant variables.

Let's say that we have created 3 action nodes CheckCloseEnemies, AttackTarget and Patrol, to exemplify on the next section.

### 2. Create the tree
On this case you must create a class that inherite from Tree class, 
next override SetupTree method, inside you must create a root node and every
node in format of Node List. 

For example:

```
protected override Node SetupTree()
    {
        Node root = new Selector(new List<Node>
        {
            new Sequence(new List<Node>
            {
                new CheckCloseEnemies(),
                new AttackTarget(),
            }),
            new Patrol(),
        }); ;

        return root;
    }
```

As you should know, Selector evaluate a new child if the previous one returned FAILURE stops evaluation otherwise.
On the other side Sequence node evaluate the new child if the previous one was evaluated to SUCCESS.

So in this case, NPC will look for enemies near him, if have someone he will try to attack him, else he will start patroling.

