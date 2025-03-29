# 阿美
阿美語語言資料庫
import { useState} from 'react'; import {Card, CardContent, Button, Input, Label, Table, TableHead, TableRow, TableCell, TableBody, Select, Option} from '@/components/ui';

导出默认函数 CorpusManager () {const [语料库，setCorpus] = useState ([]); const [inputData, setInputData] = useState ({ word: '', partOfSpeech: '', meaning: '' }); const [searchQuery, setSearchQuery] = useState ({ word: '', partOfSpeech: ''}); const [editingIndex, setEditingIndex] = useState (null);

// 从众环境中计算统计数据 = () => {const totalEntries = corpus.length; const wordFrequency = corpus.reduce ((acc, { word}) => {acc[字]   = (acc [字] || 0) + 1; return acc; }, {}); return { totalEntries, wordFrequency }; };

const handleInputChange = (e) => {const {name, value} = e.target; setInputData ({ ...inputData, [名称]: value});};

const handleSearchChange = (e) => {const {name, value} = e.target; setSearchQuery ({ ...searchQuery, [名称]: value});};

const addOrUpdateCorpus = () => { if (editingIndex !== null) {const updatedCorpus = [语料库]; 更新语料库[编辑索引] = inputData; setCorpus (updatedCorpus); setEditingIndex (null); } else {setCorpus ([... 语料库，输入数据]);} setInputData ({单词: '', partOfSpeech: '', 意思是: ''}); };

const editCorpus = (index) => {setInputData (corpus)[指数]); setEditingIndex (索引); };

const deleteCorpus = (index) => {setCorpus (corpus.filter ((_, i) => i !== index)); };

const filteredCorpus = corpus.filter (item => (searchQuery.word === '' | | item.word.includes(searchQuery.word) & (searchQuery.partOfSpeech === ' ' | item.partOfSpeech === searchQuery.partOfSpeech) );

const { totalEntries, wordFrequency} = calculateStatistics ();

 返回 ( <div 类名="p-4 space-y-4"> <卡片>   <CardContent>   <h2 类名="text-xl font-bold">語料輸入/編輯 </h2>   <div 类名="space-y-2"> <标签>詞彙</标签> <输入 name="word" value={inputData.word} onChange={handleInputChange} /> <标签>詞性</标签> <输入 name="partOfSpeech" value={inputData.partOfSpeech} onChange={handleInputChange} /> <标签>語義</标签> 输入 按钮 </按钮>   </div> </CardContent>   </卡片> 

<卡片>
    <CardContent>
 <h2 类名  ="text-xl font-bold">  语言料  </h2>
 <div 类名  ="space-y-2"> <div 类名="space-y-2">
         <标签>詞彙查詢</标签> 
 < 输入   名称=“词” 价值={searchQuery.word} onChange={handleSearchChange} /> <  输入    名称=“词” 价值={searchQuery.word} onChange={handleSearchChange} />
         <标签>詞性查詢</标签> 
 <  选择    名称=“PartOfSpeech” 价值={searchQuery.partOfSpeech} onChange={handleSearchChange}> 
 < 选项   价值="">全部</选项> 
           < 选项   价值="名詞">名詞</选项> 
           < 选项   价值="動詞">動詞</选项> 
           < 选项   价值="形容詞">形容詞</选项> 
         </选择> 
      </div>
       <桌子> 
         <桌头> 
          <TableRow>
            <TableCell>詞彙</TableCell>
            <TableCell>詞性</TableCell>
            <TableCell>語義</TableCell>
            <TableCell>操作</TableCell>
          </TableRow>
         </桌头> 
         <表体> 
 {filteredCorpus.map ((item, index) => ( 
 <TableRow 钥匙  ={索引}> 
              <TableCell>{item.word}</TableCell>
              <TableCell>{item.partOfSpeech}</TableCell>
              <TableCell>{item.me]</TableCell>
              <TableCell>
 <按钮 onClick={() => editCorpus (index)}> 小程序 </  按钮>
 <按钮 onClick={() => deleteCorpus (index)}> 重新设计 </  按钮>
              </TableCell>
            </TableRow>
           ))} 
         </表体> 
       </桌子> 
    </CardContent>
   </卡片> 

   <卡片> 
    <CardContent>
       <h2 类名="text-xl font-bold">語料統計與分析 </h2>
      <p>语言学类:{totalEntries}</p>
       <h3 类名="font-semibold">詞頻分析 </h3>
      <ul>
 {Object.entries (wordFrequency).map (([词，freq]) => (  [词，freq]) => (
 <李键 ={word}>{word}:{freq} 次 </ 李> 
         ))} 
      </ul>
    </CardContent>
   </卡片> 
</div>

); }

![图像](https://github.com/user-attachments/assets/c0b83fd1-16d2-40c2-a8da-0c6cedc65060)
