## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

#### 04. 例子

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

例子。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——Martin Fowler

#### 01. 基本信息

Martin Fowler，本书作者，大师中的大师。

#### 02. 贡献及著作

#### 03. 论文及书籍

#### 04. 演讲汇总

找一个他的 TED 演讲，有的话。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

## 书评

### 01

2009 年，在为《重构》第一版的中译本再版整理译稿时，我已经隐约察觉行业中对「重构」这个概念的矛盾张力。一方面，在这个「VUCA」（易变、不确定、复杂、模糊）横行的年代，有能力调整系统的内部结构，使其更具长期生命力，这是一个令人神往的期许。另一方面，重构的扎实工夫要学起来、做起来，颇不是件轻松的事，且不说详尽到近乎琐碎的重构手法，光是单元测试一事，怕是已有九成同行无法企及。结果，「重构」渐渐成了一块漂亮的招牌，大家都愿意挂上这个名号，可实际上干的却多是「刀劈斧砍」的勾当。

如今又是十年过去，只从国内的情况而论，「重构」概念的表里分离，大有愈演愈烈之势。随着当年的一线技术人员纷纷走上领导岗位，他们乐于将「重构」这块漂亮招牌用在更宽泛的环境下，例如系统架构、乃至组织结构，都可以「重构」一下。然而基本功的欠缺，却也一路如影随形。当年在对象中的刀劈斧砍，如今被照搬到了架构、组织的调整。于是「重构」的痛苦回忆又一遍遍重演，甚而程度更深、影响更广、为害更烈。

此时转头看 Martin Fowler 时隔将近廿载后终于付梓的《重构》第二版，我不禁感叹于他对「微末功夫」的执着。在此书尚未成型之前，我和当时 ThoughtWorks 的同事们曾有很多猜测，猜 Fowler 先生是否会在第二版中拔高层次，多谈谈设计乃至架构级别的重构手法，甚或跟随「敏捷组织」、「精益企业」的风潮谈谈组织重构，也未为不可。孰料成书令我们跌破眼镜，Fowler 先生不仅没有拔高，反而把工夫做得更扎实了。

对比前后两版的重构列表，可以发现：第二版收录的重构手法在用途上更加内聚，在操作上更加连贯，更重视重构手法之间的组合运用。第一版中占了整章篇幅的「大型重构」，在第二版中全数删去。一些较为复杂的重构手法，例如复制「被监视数据」、塑造模板函数等，第二版也不再收录。而第二版中新增的重构手法，则多是提炼变量、移动语句、拆分循环、拆分变量。

这样更加细致而微的操作。这些新增的手法看似简单，但直指大规模遗留代码中最常见的重构难点，正好补上了第一版中阙漏的细节。这一变化，正反映出 Fowler 先生对于重构一事一贯的态度：千里之行积于跬步，越是面对复杂多变的外部环境，越是要做好基本功、迈出扎实步。

坏味道、测试先行、行为保持的变更动作，是重构的基本功。在《重构》第二版里，重构手法的细节被再度打磨，重构过程比之第一版愈发流畅。细细品味重构手法中的前后步骤，琢磨作者是如何做到行为保持，这是能启发读者举一反三的读书法。举保持对象完整重构手法为例，第一版中的做法是在原本函数上新添参数；而第二版的做法则是先新建一个空函数，在其中做完想要的调整之后，再整体替换原本函数。两相对比，无疑是新的做法更加可控、出错时测试失败的范围更小。

无独有偶，我在 ThoughtWorks 时的同事王健在开展大型的架构重构时，总结了重构的「十六字心法」，恰与保持对象完整重构手法在第二版中这个新的做法暗合。这十六字心法如是说：旧的不变、新的创建、一步切换、旧的再见。

从这个视角品味一个个重构巨细靡遗的做法，读者大概能感受到重构与「刀劈斧砍」之间最根本的分歧。在很多重构（例如最常用的改变函数声明）的做法中，Fowler 先生会引入「很快就会再次修改甚至删除」的临时元素。假如只看起止状态，这些变更过程中的临时元素似乎是浪费：为何不直接一步到位改变到完善的结果状态呢？然而这些临时元素所代表的，是对变更过程（而非只是结果）的设计。缺乏对过程的精心设计与必要投入，只抱着对结果的美好憧憬提刀上阵，遇到困难就靠「奋斗精神」和加班解决，这种「刀劈斧砍」不止发生在缺乏审慎的「重构」现场，又何尝不是我们这个行业的缩影？

是以，重构这门技艺、以及 Fowler 先生撰写《重构》的态度，代表的是软件开发的匠艺 —— 对「正确的做事方式」的重视。在一个浮躁之风日盛的行业中，很多人会强调「只看结果」，轻视做事的过程与方式。然而对于软件开发的专业人士而言，如果忽视了过程与方式，也就等于放弃了我们自己的立身之本。Fowler 先生近廿载对这本书、对重构手法的精心打磨，给了我们一个榜样：一个对匠艺上心的专业人士，日积月累对过程与方式的重视，是能有所成就的。

十七年前，我以菜鸟之身读到《重构》，深受其中蕴涵的工匠精神感召，在 Fowler 先生与侯捷老师帮助下，完成了本书第一版的翻译工作。如今再译本书第二版，来自 ThoughtWorks 的青年才俊林从羽君主动请缨与我搭档合译，我亦将此视为匠艺传承的一桩美事。新一代程序员中，关注新工具、新框架、新商业模式者伙矣，关注面向对象、TDD、重构之类基本功者寥寥。林君年纪虽轻，却能平心静气磨砺技艺，对基本功学而时习，颇有老派工匠之风。当年藉由翻译《重构》一书，我从 Fowler 先生、侯捷老师身上学到他们的工匠精神，十余年来时时践行自勉。如今新一代软件工匠的代表人物林君接手此书，必会令工匠精神传承光大。

据说古时高僧有偈云：「时时勤拂拭，勿使惹尘埃」。代码当如是，专业人士的技艺亦当如是。与《重构》的诸位读者共勉。


