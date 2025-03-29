import { useState } from 'react';
import { Card, CardContent, Button, Input, Label, Table, TableHead, TableRow, TableCell, TableBody, Select, Option } from '@/components/ui';

export default function CorpusManager() {
  const [corpus, setCorpus] = useState([]);
  const [inputData, setInputData] = useState({ word: '', partOfSpeech: '', meaning: '' });
  const [searchQuery, setSearchQuery] = useState({ word: '', partOfSpeech: '' });
  const [editingIndex, setEditingIndex] = useState(null);

  // 統計數據
  const calculateStatistics = () => {
    const totalEntries = corpus.length;
    const wordFrequency = corpus.reduce((acc, { word }) => {
      acc[word] = (acc[word] || 0) + 1;
      return acc;
    }, {});
    return { totalEntries, wordFrequency };
  };

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setInputData({ ...inputData, [name]: value });
  };

  const handleSearchChange = (e) => {
    const { name, value } = e.target;
    setSearchQuery({ ...searchQuery, [name]: value });
  };

  const addOrUpdateCorpus = () => {
    if (editingIndex !== null) {
      const updatedCorpus = [...corpus];
      updatedCorpus[editingIndex] = inputData;
      setCorpus(updatedCorpus);
      setEditingIndex(null);
    } else {
      setCorpus([...corpus, inputData]);
    }
    setInputData({ word: '', partOfSpeech: '', meaning: '' });
  };

  const editCorpus = (index) => {
    setInputData(corpus[index]);
    setEditingIndex(index);
  };

  const deleteCorpus = (index) => {
    setCorpus(corpus.filter((_, i) => i !== index));
  };

  const filteredCorpus = corpus.filter(item =>
    (searchQuery.word === '' || item.word.includes(searchQuery.word)) &&
    (searchQuery.partOfSpeech === '' || item.partOfSpeech === searchQuery.partOfSpeech)
  );

  const { totalEntries, wordFrequency } = calculateStatistics();

  return (
    <div className="p-4 space-y-4">
      <Card>
        <CardContent>
          <h2 className="text-xl font-bold">語料輸入/編輯</h2>
          <div className="space-y-2">
            <Label>詞彙</Label>
            <Input name="word" value={inputData.word} onChange={handleInputChange} />
            <Label>詞性</Label>
            <Input name="partOfSpeech" value={inputData.partOfSpeech} onChange={handleInputChange} />
            <Label>語義</Label>
            <Input name="meaning" value={inputData.meaning} onChange={handleInputChange} />
            <Button onClick={addOrUpdateCorpus}>{editingIndex !== null ? '更新語料' : '新增語料'}</Button>
          </div>
        </CardContent>
      </Card>

      <Card>
        <CardContent>
          <h2 className="text-xl font-bold">語料查詢</h2>
          <div className="space-y-2">
            <Label>詞彙查詢</Label>
            <Input name="word" value={searchQuery.word} onChange={handleSearchChange} />
            <Label>詞性查詢</Label>
            <Select name="partOfSpeech" value={searchQuery.partOfSpeech} onChange={handleSearchChange}>
              <Option value="">全部</Option>
              <Option value="名詞">名詞</Option>
              <Option value="動詞">動詞</Option>
              <Option value="形容詞">形容詞</Option>
            </Select>
          </div>
          <Table>
            <TableHead>
              <TableRow>
                <TableCell>詞彙</TableCell>
                <TableCell>詞性</TableCell>
                <TableCell>語義</TableCell>
                <TableCell>操作</TableCell>
              </TableRow>
            </TableHead>
            <TableBody>
              {filteredCorpus.map((item, index) => (
                <TableRow key={index}>
                  <TableCell>{item.word}</TableCell>
                  <TableCell>{item.partOfSpeech}</TableCell>
                  <TableCell>{item.meaning}</TableCell>
                  <TableCell>
                    <Button onClick={() => editCorpus(index)}>編輯</Button>
                    <Button onClick={() => deleteCorpus(index)}>刪除</Button>
                  </TableCell>
                </TableRow>
              ))}
            </TableBody>
          </Table>
        </CardContent>
      </Card>

      <Card>
        <CardContent>
          <h2 className="text-xl font-bold">語料統計與分析</h2>
          <p>總語料數：{totalEntries}</p>
          <h3 className="font-semibold">詞頻分析</h3>
          <ul>
            {Object.entries(wordFrequency).map(([word, freq]) => (
              <li key={word}>{word}：{freq} 次</li>
            ))}
          </ul>
        </CardContent>
      </Card>
    </div>
  );
}
![image](https://github.com/user-attachments/assets/63310999-1ad3-4041-ac62-806d1c5b8ffa)
