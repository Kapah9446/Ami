// GitHub 語言資料管理系統 - Ami 語料庫 // 功能：語料新增、編輯、刪除、查詢、版本控制 // 適合團隊協作與遠端貢獻

const fs = require('fs'); const path = require('path');

// 語料庫資料夾 const CORPUS_DIR = path.join(__dirname, 'Ami');

// 初始化語料庫 function initCorpus() { if (!fs.existsSync(CORPUS_DIR)) { fs.mkdirSync(CORPUS_DIR); console.log('Ami 語料庫已建立'); } else { console.log('Ami 語料庫已存在'); } }

// 新增語料 function addCorpus(id, data) { const filePath = path.join(CORPUS_DIR, ${id}.json); fs.writeFileSync(filePath, JSON.stringify(data, null, 2)); console.log('語料已新增:', id); }

// 查詢語料 function getCorpus(id) { const filePath = path.join(CORPUS_DIR, ${id}.json); if (fs.existsSync(filePath)) { const data = JSON.parse(fs.readFileSync(filePath)); console.log('語料查詢結果:', data); return data; } else { console.log('無此語料'); } }

// 刪除語料 function deleteCorpus(id) { const filePath = path.join(CORPUS_DIR, ${id}.json); if (fs.existsSync(filePath)) { fs.unlinkSync(filePath); console.log('語料已刪除:', id); } else { console.log('無此語料'); } }

// 語料列表 function listCorpus() { const files = fs.readdirSync(CORPUS_DIR); console.log('Ami 語料庫目錄:'); files.forEach(file => console.log(file)); }

// 初始化 initCorpus();

// 測試 addCorpus('example1', { word: 'takici', partOfSpeech: 'verb', meaning: 'to speak' }); getCorpus('example1'); listCorpus(); deleteCorpus('example1'); listCorpus();

