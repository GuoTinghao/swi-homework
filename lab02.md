用Constuct2制作一个简单的游戏
# 首先，新建一个项目：
![](/Users/asus/Desktop/fiblenew.png)
## 然后双击画布
![](/Users/asus/Desktop/insertobject.png)
选择Tiled Background。这时，鼠标指针形状变成了十字形，你可以在布局的任何位置点击，我们在布局中间差不多位置
点击，弹出Texture editor对话框，我们点击打开文件夹图标，选择一个背景
接下来把背景调到适应画布： 
点击背景，在右侧属性框把Size改为（1280,1024）。 
![](/Users/asus/Desktop/tiledproperties.png)
接下来，我们来添加更多的对象。首先我们先去把背景瓦片对象锁定了，这样才不会被我们再次选中，和PS,FL里的锁定一样。
画布由多个层组成，我们可以在不同的层放置不同的对象，可以通过调整层的上下顺序来调整对象的前后显示，层可以被隐藏或者锁定，平滚特效等。背景瓦片放置于最底层，其他对象如玩家，怪物，NPC等放置在上面的几层。

我们可以通过Layers tab来管理层，和Project bar工程面板在一个选项卡中。 
![](/Users/asus/Desktop/layerstab.png)
点击layer，将背景layer1更名为Background并锁定。然后新加入一个层layer2，我们将要在这个层上进行主要的操作。
# 添加输入控制对象
## 回到画布中，同样双击插入另外一个对象，这次我们选择Mouse对象，我们需要鼠标输入控制。同样的添加Keyboard对象。 
注意：这些对象不需要置于画布中，他们是隐藏的，自动在工程中起作用，现在工程中的所有层都可以使用鼠标和键盘输入控制了。
# 游戏对象
## 添加游戏对象了，如玩家角色，怪物角色，子弹，游戏特效
对于这些对象，我们用sprite（精灵）对象来置入，方法跟背景和Mouse对象一样： 
1、双击插入新对象 
2、双击选择Sprite对象 
3、当鼠标变成十字，在画布中点击 
4、弹出对话框，点击open 图标，加载四张素材图片中的一张 
5、保存并关闭对话框 
然后将子弹和爆炸移到画布外，因为刚开始我们看不到。 
默认CT2会自动把我们的对象命名为Sprite,Sprite2,Sprite3,Sprite4，我们可以在他们各自的Properties bar属性面板里的Name属性里更改为玩家，怪物，子弹，爆炸特效。
# 添加行为
## 我们给玩家添加8 direction movement行为：选择玩家，在properties bar属性面板里，找到Behaviors分类，点击Add/Edit弹出Behaviors行为对话框。
点击绿色加号，双击8 direction movement。
接着以同样的方法给玩家添加Scroll To和Bound to layout行为，
我们以同样的方法给其他对象添加相应的行为如下:
-给子弹对象添加Bullet movement和Destroy outside layout行为。 
-给怪物对象添加Bullet movement行为。 
-给爆炸特效对象添加Fade行为。Fade行为默认会销毁对象，所以不用担心对象有没有销毁。
# 添加更多怪物
## 按住CTRL，拖拽Monster对象复制几个实例。他们都是Monster对象类型的。
# 添加事件
## 我们来创建第一个事件 
我们将使玩家（发射口）一直看向鼠标，这样我们点击发射子弹的时候，子弹将发往鼠标方向。
在event sheet的空白位置双击，将打开添加事件对话框。
不同的对象根据他们要做的行为拥有不同的条件和动作，在对话框中双击System对象，对话框中列出了所有System对象的条件。
双击Every tick条件插入到事件表中。对话框将关闭，Every tick事件被创建，但没有actions(动作)。
对话框中列出了可以添加动作的对象，双击玩家对象，
选取Set angle towards position动作。该动作会自动计算角色到给定的X,Y坐标的角度。
接下来要指定X,Y坐标值（动作的参数，条件同样可以带有参数）。我们输入Mouse.X和Mouse.Y，点击对话框上的Done确定按钮。该动作就被添加了！
同理，我们继续给对象添加事件： 
让角色可以射击 
当玩家点击的时候，可以发射子弹。这可以通过Spawn an object动作来实现，该动作在同样的位置和角度（相对于角色）创建新的对象实例。子弹的Bullet movement属性将会使它向前飞出。
步骤如下：条件：Mouse->On click->Left clicked(the default) 
//鼠标->点击->左击（默认） 
动作：玩家->Spawn another object->For Object，choose 子弹  
//玩家->产生另外的对象->对象，选择子弹层，输入1（“layer2”图层）,Image point（子弹的发射起点）保持默认为0。
条件：子弹->On collision with another object->pick 怪物。 
//子弹->于其他对象碰撞->选择怪物。 
动作：怪物->Destroy 
//怪物->消灭 
动作：子弹->Spawn another object->Explosion，layer 1 
//在图层1 碰撞的位置产生新对象-爆炸特效 
动作：子弹->Destroy 


当下怪物只会向右移动。我们来让他们更有趣些。首先让他们产生在随机的位置。 
条件：System->On start of Layout 
//系统->画布启动时 
动作：怪物->Set angle->random(360) 
//怪物->设置角度->0-360随机度数 
Condition: System -> On start of Layout 
Action: 怪物r -> Set angle -> random(360) 
此时，怪物依然移出画布，再也看不到，接着我们再来修改，让怪物移动边缘处的时候，自动往回移动，并且添加智能，让怪物朝着玩家角色移动（自然是角色没挂的时候）。 
条件：怪物->Is outside layout 
//判断怪物是否要离开画布 
动作：怪物->Set angle toward position->For X，玩家.X - for Y,玩家.Y 
//设置怪物朝向角色的坐标
到这，游戏就大概成型了。下图是我的游戏jpg
![](/Users/asus/Desktop/1.jpg)

