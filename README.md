- 搜狗实验室数据资源 （http://www.sogou.com/labs/）  
>1. 包含了5大类13种数据资源  
>>1.1 评测集合   
>>>1.1.1 搜索结果评价   
>>>>简介：判断搜索结果与查询的相关性，是否符合搜索意图。  
>>>>数据：完整版4326条，数据格式“查询词\相关的URL\查询类别”。  
>>>>相关技术：2.1。   
>>>1.1.2 话题跟踪及检测评价   
>>>>简介：评测新闻话题跟踪及检测效果。  
>>>>数据：完整版953条，数据格式“URL\话题名称”。
>>>>相关技术：2.2
>>>1.1.3 文本分类评价 
>>>>简介：评估文本分类结果的正确性。语料来自搜狐等多个新闻网站近20个频道。    
>>>>数据：94条，数据格式“URL前缀\对应类别标记”。（其中“URL前缀”对应的数据放在“全网新闻数据”或“搜狐新闻数据”中出现）  
>>1.2 语料数据  
    1.2.1 互联网语料库        
    1.2.2 链接关系库  
    1.2.3 SogouRank库  
    1.2.4 用户查询日志  
  1.3 新闻数据  
    1.3.1 全网新闻数据  
    1.3.2 搜狐新闻数据  
  1.4 图片数据  
    1.4.1 互联网图片库  
    1.4.2 互联网图片库2.0  
  1.5 自然语言处理相关数据  
    1.5.1 互联网词库  
    1.5.2 中文词语搭配库  
2. 相关技术
  - 基于点击数据分析，自动对搜索结果进行评估。(http://www.sogou.com/labs/paper/Automatic_Search_Engine_Performance_Evaluation_with_Click-through_Data_Analysis.pdf)   
    1. 将搜索分成三种情况：找特定网址、找信息、处理事务。“找特定网址”具有明确的目标特征。因此仅考虑这类搜索情况。  
    2. 通过统计搜索词q与搜索结果中点击量最多的链接r，统计（q，r），并在下次给出搜索结果时让r更靠前，如此不断验证。  
    3. 从2006年6月至2007年1月，对sougou.com的检索和点击数据进行统计。  
    4. 准确率为97%左右。错误结果中，一些网址是正确网址的子网站。例如，搜索163通常会定位到163邮箱mail.163.com，而非www.163.com。        
  - 网络环境下自动进行在线新闻事件的生成。(http://www.sogou.com/labs/paper/Automatic_Online_News_Issue_Construction_in_Web_Environment.pdf)    
    1. 方法分三步：  
      1）话题检测，将新出现的文本内容聚类成候选话题。  
      2）话题对比，候选话题与既有的话题比较，并入既有话题或称为新的话题。  
      3）根据相关话题生成新闻事件。  
    2. 具体做法：   
      1）预处理：提取页面内容，分句，除去无用句，对单词进行标记（中文进行词汇划分），词性标注，识别命名实体，删除“应删除词”（例如“的”），最终每篇文章生成一个词向量。  
      2）计算t时刻词w的“词频”，每篇文章表示表示为t时刻的一个n维向量，使用增量TF-IWF模型计算各维度权重weight t(d,w)并归一化处理。  
      3）使用余弦相似度算法计算两篇文章间的相似度。  
      4）使用算术平均加权配对组（UPGMA）的聚类方法，将新文章聚类至候选话题中。    
      5）对候选话题与既有话题相比较，并入并更新既有话题，或成为新的话题。  
      6）类似地将各话题聚类到新闻事件中，并不断更新新闻事件或生成新的新闻事件。    
      7）自动对各新闻事件加入网络上的相关博文、评论和图片、音视频等。 
    3. 实验数据：
      数据集1：含350个新闻页面，87个话题。2007年3月到4月，均关于搜索引擎公司。中文新闻网站，包括新闻报道和新闻回顾。最多的话题包含20个文章，最少的仅1个。  
      数据集2：含953个新闻页面，108个话题。2007年4月22日的搜狐体育新闻频道。最大话题有151个文章，最少的1个。  
      数据集3：含24872个新闻页面，选自多个中文新闻网站和1339篇博文和评论文章。
    4. 结果：  
      1）聚类方法的选择：direct-I2-IDF、direct-I2-IWF、rbr-H2-IDF、rbr-H2-IWF、graph-jacc-IDF、graph-jacc-IWF、agglo-upgma-IDF、agglo-upgma-IWF这八个算法中，“aggloupgma-IWF”算法更优。  
      2）IWF与IDF比较：IWF模型的效果更平滑更优。  
      3）冗余句子的去除（RSR）：新闻中冗余句子较少，RSR有效果但不明显。  
      4）标题的使用及权重：加标题表现更好；仅短文加标题比全部加标题更好；标题权重比正文相对更大表现更好。
      
### 搜狗实验室数据资源 （http://www.sogou.com/labs/）  
	1. 包含了5大类13种数据资源  
		1.1 评测集合   
			1.1.1 搜索结果评价   
				简介：判断搜索结果与查询的相关性，是否符合搜索意图。  
				数据：完整版4326条，数据格式“查询词\t相关的URL\t查询类别”。  
				相关任务：基于互联网预料的信息检索。  
				相关技术：2.1。   
			1.1.2 话题跟踪及检测评价   
				简介：评测新闻话题跟踪及检测效果。  
				数据：完整版953条，数据格式“URL\t话题名称”。  
				相关任务：文本分类。  
				相关技术：2.2  
			1.1.3 文本分类评价   
				简介：评估文本分类结果的正确性。    
				数据：94条，数据格式“URL前缀\t对应类别标记”。  
				相关任务：文本分类。  
		1.2 语料数据   
			1.2.1 互联网语料库  
				简介：来自互联网各种类型的1.3亿个原始网页。  
				数据：完整版1TB，迷你版10个页面数据。  
				相关任务：相关性排序，文本分类，新词发现，机器翻译，分词。  
				相关技术：2.3，2.4      
			1.2.2 链接关系库  
				简介：包括对应互联网语料库内文档的链接关系列表。  
				数据：完整版90GB，迷你版1000条URL对照表和1000条链接关系。  
				相关任务：相关行排序，链接分析，反垃圾。  
				相关技术：2.4  
			1.2.3 SogouRank库  
				简介：互联网语料库中各页面的重要程度评级。  
				数据：完整版90GB，迷你版1001条，数据格式“URL\tSougouRank”。  
				相关任务：相关行排序。  
			1.2.4 用户查询日志  
				简介：搜索引擎部分网页查询需求及用户点击情况的网页查询日志数据。  
				数据：完整版1.9GB，迷你版10000条，数据格式“访问时间\t用户ID\t[查询词]\t该URL在返回结果中的排名\t用户点击的顺序号\t用户点击的URL”。  
				相关任务：相关行排序，用户兴趣挖掘，查询扩展，新词发现。  
		1.3 新闻数据  
			1.3.1 全网新闻数据  
				简介：来自5个新闻站点共83个频道的新闻数据，提供URL和正文信息。  
				数据：完整版1.02GB，迷你版200条新闻数据。  
				相关任务：文本分类，事件检测跟踪，新词发现，命名实体识别，自动摘要。  
				相关技术：2.2  
			1.3.2 搜狐新闻数据  
				简介：来自搜狐新闻共18个频道的新闻数据，提供URL和正文信息。  
				数据：完整版65GB，迷你版200条新闻数据，论文（2.2）版953条。 
				相关任务：文本分类，事件检测跟踪，新词发现，命名实体识别，自动摘要。  
				相关技术：2.2  
		1.4 图片数据  
			1.4.1 互联网图片库  
				简介：来自sougou图片搜索索引的280多万张抓取图片及标注数据集合。    
				数据：完整版269GB。  
				相关任务：基于文本/内容的图片检索。  
			1.4.2 互联网图片库2.0  
				简介：1000万张互联网图片和相关文本信息，以及识图搜索结果的人工标注集合。    
				数据：完整版635GB。  
				相关任务：基于内容的图片检索。  
		1.5 自然语言处理相关数据   
			1.5.1 互联网词库  
				简介：基于互联网语料环境的高频词对应的词频、词性信息。      
				数据：完整版1.3MB，共157202个词。  
				相关任务：中文词性标注，词频分析。  
			1.5.2 中文词语搭配库  
				简介：基于互联网语料的字词搭配关系统计。        
				数据：完整版共18399496组，迷你版共100000组。  
				相关任务：中文输入法，文字到语音转化，语音识别。  
				相关技术：2.5，2.6  
	2. 提出了一些相关技术与实验  
		2.1 基于点击数据分析，自动对搜索结果进行评估。(http://www.sogou.com/labs/paper/Automatic_Search_Engine_Performance_Evaluation_with_Click-through_Data_Analysis.pdf)   
			将搜索分成三种情况：找特定网址、找信息、处理事务。“找特定网址”具有明确的目标特征。因此仅考虑这类搜索情况。  
			通过统计搜索词q与搜索结果中点击量最多的链接r，统计（q，r），并在下次给出搜索结果时让r更靠前，如此不断验证。  
			从2006年6月至2007年1月，对sougou.com的检索和点击数据进行统计。  
			准确率为97%左右。错误结果中，一些网址是正确网址的子网站。例如，搜索163通常会定位到163邮箱mail.163.com，而非www.163.com。        
		2.2 网络环境下自动进行在线新闻事件的生成。(http://www.sogou.com/labs/paper/Automatic_Online_News_Issue_Construction_in_Web_Environment.pdf)    
			方法分三步：  
				1）话题检测，将新出现的文本内容聚类成候选话题。  
				2）话题对比，候选话题与既有的话题比较，并入既有话题或称为新的话题。  
				3）根据相关话题生成新闻事件。  
			具体做法：   
				1）预处理：提取页面内容，分句，除去无用句，对单词进行标记（中文进行词汇划分），词性标注，识别命名实体，删除“应删除词”（例如“的”），最终每篇文章生成一个词向量。  
				2）计算t时刻词w的“词频”，每篇文章表示表示为t时刻的一个n维向量，使用增量TF-IWF模型计算各维度权重weight t(d,w)并归一化处理。  
				3）使用余弦相似度算法计算两篇文章间的相似度。  
				4）使用算术平均加权配对组（UPGMA）的聚类方法，将新文章聚类至候选话题中。    
				5）对候选话题与既有话题相比较，并入并更新既有话题，或成为新的话题。  
				6）类似地将各话题聚类到新闻事件中，并不断更新新闻事件或生成新的新闻事件。    
				7）自动对各新闻事件加入网络上的相关博文、评论和图片、音视频等。 
			实验数据：  
				数据集1：含350个新闻页面，87个话题。2007年3月到4月，均关于搜索引擎公司。中文新闻网站，包括新闻报道和新闻回顾。最多的话题包含20个文章，最少的仅1个。  
				数据集2：含953个新闻页面，108个话题。2007年4月22日的搜狐体育新闻频道。最大话题有151个文章，最少的1个。  
				数据集3：含24872个新闻页面，选自多个中文新闻网站和1339篇博文和评论文章。  
			结果：  
				1）聚类方法的选择：direct-I2-IDF、direct-I2-IWF、rbr-H2-IDF、rbr-H2-IWF、graph-jacc-IDF、graph-jacc-IWF、agglo-upgma-IDF、agglo-upgma-IWF这八个算法中，“aggloupgma-IWF”算法更优。  
				2）IWF与IDF比较：IWF模型的效果更平滑更优。  
				3）冗余句子的去除（RSR）：新闻中冗余句子较少，RSR有效果但不明显。  
				4）标题的使用及权重：加标题表现更好；仅短文加标题比全部加标题更好；标题权重比正文相对更大表现更好。    
		2.3 使用与查询无关的特征对网络信息检索数据进行清洗。(http://www.sogou.com/labs/paper/Data_Cleansing_for_Web_Information_Retrieval_using_Query_Independent_Features.pdf)  
			若使用普通的链接分析方法，基于网页的被点击概率，而非页面的有用度。因此使用与查询无关的特征。  
			结合利用了链接分析和页面布局分析，进行全局规模的数据清洗。  
			使用朴素贝叶斯学习算法，在低维度实例空间上高效实用，且不需要原有数据集的先验知识。  
			将5个特征：文字长度，链接文本长度，搜索排名值，导入链接数量和导出链接数量综合应用，比仅使用单独一个特征效果更好。  
			清洗后选出的高质量页面占全部的52%（.GOV数据集）和5%（sogou数据集），召回率>90%。即牺牲了10%的正确搜索结果，大大节省了存储空间。  
			同时能够消除30%的垃圾页面和15%的低质量页面。  
		2.4 一种基于链接分析的垃圾页面检测算法。（http://www.sogou.com/labs/paper/R-SpamRank_A_Spam_Detection_Algorithm_Based_on_Link_Analysis.pdf）  
			一些人试图误导搜索引擎以提升网页的搜索排名，方法主要是基于内容和基于链接两种。这里提出一种半自动的检测这种垃圾网页的方法。  
			使用人工识别的垃圾页面黑名单作为种子，根据链接到本页面的情况，反向传播RSR值，并不断迭代直到各页面值稳定。  
			测试数据为sogou.com的500万个网页，迭代50次。人工分析后，不能打开的页面赋值0，好的页面赋值1，半垃圾页面赋值2，纯垃圾页面赋值3。  
			将结果中RSR值最高的1万个页面中的前100个和最后100个取出做人工检查。发现99%是垃圾页面。证明算法有效。  
			发现垃圾页面集中在两个域名，说明算法能够检测链接工厂。  
			做域名清理，即删除3个链接工厂下的所有页面后再分析。剩下的178个页面中仍有87.1%的垃圾页面。  
			前5大链接工厂产生了99.1%的垃圾页面。  
		2.5 基于相对条件熵的搭配抽取方法。（http://www.sogou.com/labs/paper/Wangdaliang_JoBUPT_07.pdf）   
			在自然语言处理中，研究搭配组词项之间的内在倾向性。提出使用相对条件熵比传统的使用互信息评价二元相关性更优。  
			词语在语料库中出现越频繁，越容易失去倾向的特性。  
			绝大多数次的左搭配力大于自己的右搭配力。  
			左搭配倾向强的多是定语；右搭配倾向抢的多是宾语。  
			自然文本的搭配抽取方法：  
				1）预处理。提取文本，分词，词性标注，停用词过滤，词频过滤。    
				2）数据统计。利用词性过滤模板、滑动窗口生成搭配候选二元组统计矩阵，同时统计二元同现次数、构成次的词频以及样本总词频。  
				3）搭配抽取。计算候选二元组左、右搭配倾向强度以及搭配整合强度，依据阈值输出搭配抽取结果。  
			对sogou.com的1亿多个中文页面语料库数据进行实验。预处理得搭配候选二元组35万个，自动获取搭配词对3.5万个。人工验证得效果比互信息法好。  
		2.6 多策略融合的搭配抽取方法。（http://www.sogou.com/labs/paper/Wangdaliang_JoTHU_08.pdf）  
			搭配抽取中，需要识别频繁二元组和稀疏二元组，而排除无关二元组。  
			互信息法可作为二元组无关性的度量方法，用于排除大部分无关二元组。  
			卡方检验法比t检验法更适合于刻画二元组的相关性，且能很好识别频繁二元组，但对稀疏二元组不行。  
			对数似然比检验法可用于识别稀疏二元组。  
			对sogou.com的1亿多个中文页面语料库数据进行实验。预处理得搭配候选二元组35万个，自动获取搭配词对5万个。人工验证得多策略融合法效果更好。  
