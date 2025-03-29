从 “反应” 导入 { useState};
import {卡，CardContent, 按钮，输入，标签，表，表头，表行，表单元，表体，选择，选项} from '@/components/ui';

导出默认函数 CorpusManager () {
 康斯特 [语料库，setCorpus] = useState ([]);
 康斯特 [inputData, setInputData] = useState ({单词: '', partOfSpeech: '', 意思是: ''});
 康斯特 [searchQuery, setSearchQuery] = useState ({单词: '', partOfSpeech: ''});
 康斯特 [editingIndex, setEditingIndex] = useState (null);

   // 統計數據 
 const calculateStatistics = () => { 
 const totalEntries = corpus.length; 
 const wordFrequency = corpus.reduce ((acc, {word}) => { 
 acc [字]   = (acc [字]   || 0) + 1; 
 返回 acc; 
     }, {}); 
 return { totalEntries, wordFrequency}; 
   }; 

 const handleInputChange = (e) => { 
 const {name, value} = e.target; 
 setInputData ({ ...inputData, [名称]: 值});
   }; 

 const handleSearchChange = (e) => { 
 const {name, value} = e.target; 
 setSearchQuery ({ ...searchQuery, [名称]: 值});
   }; 

 const addOrUpdateCorpus = () => { 
 if (editingIndex !== null) { 
 const updatedCorpus = [语料库];
  更新语料库  [编辑索引] = inputData;
 setCorpus (updatedCorpus); 
 setEditingIndex (null); 
 } 其他 { 
 setCorpus ( [... 语料库，输入数据]);
     } 
 setInputData ({单词: '', partOfSpeech: '', 意思是: ''}); 
   }; 

 const editCorpus = (索引) => { 
 setInputData (语料库) [指数]);
 setEditingIndex (索引); 
   }; 

 const deleteCorpus = (索引) => { 
 setCorpus (corpus.filter ((_, i) => i !== index)); 
   }; 

 const filteredCorpus = corpus.filter (item => 
 (searchQuery.word === '' | | item.word.includes(searchQuery.word) && 
 (searchQuery.partOfSpeech === '' || item.partOfSpeech === searchQuery.partOfSpeech) 
   ); 

 const { totalEntries, wordFrequency} = calculateStatistics (); 

 返回 ( 
 <div 类名  ="p-4 space-y-4"> 
       <卡片> 
        <CardContent>
           <h2 类名="text-xl font-bold">語料輸入/編輯  </h2>
 <div 类名  ="space-y-2"> 
             <标签>詞彙</标签> 
 < 输入   名称=“词” 价值={inputData.word} onChange={handleInputChange} /> < 输入   名称=“词” 价值={inputData.word} onChange={handleInputChange} />
             <标签>詞性</标签> 
 <  输入    名称=“PartOfSpeech” 价值={inputData.partOfSpeech} onChange={handleInputChange} /> <  输入    名称=“PartOfSpeech” 价值={inputData.partOfSpeech} onChange={handleInputChange} />
             <标签>語義</标签> 
 < 输入   名称=“意义” 价值={inputData.me] onChange={handleInputChange} /> 
 <按钮  onClick={addOrUpdateCorpus}>{editingIndex !== null ? '更新語料' : '新增語料'}  
          </div>
        </CardContent>
       </卡片> 

     <卡片> 
     <CardContent> 
           <h2 className="text-xl font-bold">語料查詢</h2> 
     <div className="space-y-2"> 
             <Label>詞彙查詢</Label> 
     <Input name="word" value={searchQuery.word} onChange={handleSearchChange} /> 
             <Label>詞性查詢</Label> 
     <Select name="partOfSpeech" value={searchQuery.partOfSpeech} onChange={handleSearchChange}> 
     <Option value="> 全部 </Option> 
               <Option value="名詞">名詞</Option> 
               <Option value="動詞">動詞</Option> 
               <Option value="形容詞">形容詞</Option> 
     </ 选择> 
     </div> 
     <表> 
     <TableHead> 
     <TableRow> 
                 <TableCell>詞彙</TableCell> 
                 <TableCell>詞性</TableCell> 
                 <TableCell>語義</TableCell> 
     <TableCell> 操作 </TableCell> 
     </TableRow> 
     </TableHead> 
     <TableBody> 
     {filteredCorpus.map ((item, index) => ( 
     <TableRow key={index}> 
     <TableCell>{item.word}</TableCell> 
     <TableCell>{item.partOfSpeech}</TableCell> 
     <TableCell>{item.meaning}</TableCell> 
     <TableCell> 
     <Button onClick={() => editCorpus (index)}> ˤ� </Button> 
     <Button onClick={() => deleteCorpus (index)}> ɇ�</Button> 
     </TableCell> 
     </TableRow> 
               ))} 
     </TableBody> 
     </ 表> 
     </CardContent> 
     </ 卡> 

     <卡片> 
     <CardContent> 
           <h2 className="text-xl font-bold">語料統計與分析</h2> 
     <p> 语言语料数:{totalEntries}</p> 
           <h3 className="font-semibold">詞頻分析</h3> 
     <ul> 
     {Object.entries (wordFrequency).map (([word, freq]) => ( 
     <li key={word}>{word}:{freq} 次 </li> 
             ))} 
     </ul> 
     </CardContent> 
     </ 卡> 
    </div>
   ); 
}
