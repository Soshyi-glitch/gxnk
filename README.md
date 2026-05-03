# gxnk
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>门店调拨系统 | 借还管理 + 产品编码</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }
        body {
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
            background: #f4f9fe;
            color: #1e2f3e;
            padding: 12px 10px 32px;
        }
        .container {
            max-width: 1300px;
            margin: 0 auto;
        }
        .app-header {
            background: white;
            border-radius: 28px;
            padding: 12px 16px;
            margin-bottom: 20px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.02);
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
        }
        .title h1 {
            font-size: 1.35rem;
            font-weight: 700;
            background: linear-gradient(135deg, #1e4a76, #2c6e9e);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
        }
        .title p {
            font-size: 0.65rem;
            color: #5a6e8a;
        }
        .header-buttons {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }
        .btn-icon {
            background: #f0f2f5;
            border: none;
            padding: 6px 12px;
            border-radius: 40px;
            font-weight: 500;
            font-size: 0.7rem;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 4px;
            transition: 0.2s;
            color: #1f2f4a;
        }
        .btn-primary {
            background: #1e3a8a;
            color: white;
        }
        .btn-primary:hover {
            background: #1e40af;
        }
        .btn-danger {
            background: #b91c1c;
            color: white;
        }
        .card {
            background: white;
            border-radius: 24px;
            padding: 16px 18px;
            margin-bottom: 20px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.02), 0 1px 2px rgba(0,0,0,0.03);
        }
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            margin-bottom: 14px;
            border-bottom: 1px solid #e9eef3;
            padding-bottom: 10px;
        }
        .card-header h2 { font-size: 1.2rem; font-weight: 600; }
        .form-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 14px;
            margin-bottom: 16px;
        }
        @media (min-width: 640px) {
            .form-grid { grid-template-columns: repeat(2, 1fr); gap: 16px; }
        }
        @media (min-width: 900px) {
            .form-grid { grid-template-columns: repeat(3, 1fr); }
        }
        .input-group {
            display: flex;
            flex-direction: column;
            gap: 6px;
            position: relative;
        }
        .input-group label {
            font-weight: 600;
            font-size: 0.75rem;
            color: #334155;
        }
        select, input, button {
            padding: 10px 12px;
            border-radius: 20px;
            border: 1px solid #cfdfed;
            font-family: inherit;
            font-size: 0.85rem;
            background: white;
            width: 100%;
        }
        button {
            background: #1e3a8a;
            color: white;
            font-weight: 600;
            border: none;
            cursor: pointer;
            justify-content: center;
        }
        .btn-outline {
            background: white;
            border: 1px solid #cbd5e1;
            color: #1f2f4e;
        }
        .btn-sm {
            padding: 6px 12px;
            font-size: 0.7rem;
            border-radius: 30px;
        }
        .radio-group {
            display: flex;
            gap: 16px;
            align-items: center;
            background: #f9fafc;
            padding: 6px 12px;
            border-radius: 40px;
        }
        .radio-group label {
            font-weight: normal;
            display: flex;
            align-items: center;
            gap: 6px;
            cursor: pointer;
        }
        .search-dropdown {
            position: absolute;
            top: 100%;
            left: 0;
            right: 0;
            background: white;
            border: 1px solid #dce5f0;
            border-radius: 20px;
            max-height: 200px;
            overflow-y: auto;
            z-index: 20;
            box-shadow: 0 8px 20px rgba(0,0,0,0.1);
            margin-top: 4px;
        }
        .search-item {
            padding: 8px 12px;
            cursor: pointer;
            border-bottom: 1px solid #f0f4fa;
            font-size: 0.8rem;
        }
        .search-item:hover {
            background: #eef3ff;
        }
        .table-wrapper {
            overflow-x: auto;
            border-radius: 18px;
            margin-top: 8px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.7rem;
            min-width: 680px;
        }
        th, td {
            padding: 10px 6px;
            text-align: left;
            border-bottom: 1px solid #ecf3fa;
        }
        th {
            background: #f8fafd;
            font-weight: 600;
        }
        .badge-cat {
            background: #eef2ff;
            padding: 3px 10px;
            border-radius: 30px;
            font-size: 0.65rem;
            display: inline-block;
        }
        .badge-borrow { background: #fff3e3; color: #b45309; }
        .badge-return { background: #e0f2fe; color: #0369a1; }
        .modal-mask {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            backdrop-filter: blur(4px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 12px;
        }
        .modal-container {
            background: white;
            max-width: 95vw;
            width: 800px;
            max-height: 85vh;
            border-radius: 28px;
            overflow-y: auto;
            padding: 18px 16px;
        }
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 14px;
            padding-bottom: 10px;
            border-bottom: 1px solid #e2e8f0;
        }
        .close-modal {
            background: none;
            font-size: 24px;
            cursor: pointer;
            color: #7e8cae;
            padding: 0;
            width: auto;
        }
        .product-item, .shop-item, .borrow-item {
            background: #fafcff;
            border-radius: 18px;
            padding: 8px 12px;
            margin-bottom: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid #eef2fc;
        }
        .footer-note {
            font-size: 0.65rem;
            text-align: center;
            color: #6c7f99;
            margin-top: 16px;
        }
        .version-info {
            text-align: center;
            font-size: 0.6rem;
            color: #8ba0bc;
            margin-top: 16px;
        }
        .info-note {
            font-size: 0.7rem;
            background: #eef2ff;
            padding: 5px 10px;
            border-radius: 16px;
        }
    </style>
    <script src="https://cdn.sheetjs.com/xlsx-0.20.2/package/dist/xlsx.full.min.js"></script>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>
<div id="app">
    <div class="container">
        <div class="app-header">
            <div class="title">
                <h1>🏪 门店智能调拨 · 借还闭环</h1>
                <p>产品编码｜借还配对｜报表自动抵消</p>
            </div>
            <div class="header-buttons">
                <button class="btn-icon" @click="openProductManager">📦 产品库 (含编码)</button>
                <button class="btn-icon" @click="openShopManager">🏬 门店管理</button>
                <button class="btn-icon btn-primary" @click="openFullReportModal">📊 报表(未结清)</button>
            </div>
        </div>

        <!-- 登记调拨表单 -->
        <div class="card">
            <div class="card-header">
                <h2>✍️ 登记借/还调拨</h2>
                <span class="badge-cat">借 → 归还后自动抵消，报表隐藏</span>
            </div>
            <div class="form-grid">
                <div class="input-group">
                    <label>🏪 调出门店 (借出方/归还方)</label>
                    <select v-model="form.outShop">
                        <option value="">--请选择--</option>
                        <option v-for="shop in shopList" :value="shop">{{ shop }}</option>
                    </select>
                </div>
                <div class="input-group">
                    <label>📍 调入门店 (借入方/接收方)</label>
                    <select v-model="form.inShop">
                        <option value="">--请选择--</option>
                        <option v-for="shop in shopList" :value="shop">{{ shop }}</option>
                    </select>
                </div>
                <div class="input-group">
                    <label>🏷️ 产品类别</label>
                    <select v-model="form.category" @change="onCategoryChange">
                        <option value="">--选择类别--</option>
                        <option v-for="cat in allCategories" :value="cat">{{ cat }}</option>
                    </select>
                </div>
                <div class="input-group">
                    <label>🔍 产品名称 / 编码</label>
                    <input type="text" 
                           v-model="productKeyword" 
                           @input="onProductKeywordInput" 
                           @focus="showProductDropdown = true"
                           @blur="handleDropdownBlur"
                           placeholder="输入名称或编码搜索" 
                           autocomplete="off">
                    <div v-if="showProductDropdown && filteredSearchProducts.length > 0" class="search-dropdown">
                        <div v-for="prod in filteredSearchProducts" :key="prod.id" class="search-item" @mousedown.prevent="selectProduct(prod)">
                            <strong>{{ prod.name }}</strong> <span style="color:#6c7a91;">({{ prod.code }})</span> <span style="font-size:0.65rem;">{{ prod.spec }}</span>
                        </div>
                    </div>
                    <div v-if="form.selectedProductName" style="font-size:0.7rem; color:#1e5a8a;">已选：{{ form.selectedProductName }} (编码:{{ form.productCode }})</div>
                </div>
                <div class="input-group">
                    <label>🔢 产品编码 (自动带出)</label>
                    <input type="text" v-model="form.productCode" readonly disabled style="background:#f9fafb;">
                </div>
                <div class="input-group">
                    <label>📏 规格</label>
                    <input type="text" v-model="form.spec" readonly disabled style="background:#f9fafb;">
                </div>
                <div class="input-group">
                    <label>🔢 数量</label>
                    <input type="number" v-model.number="form.quantity" min="0.1" step="1" placeholder="数量">
                </div>
                <div class="input-group">
                    <label>📅 日期</label>
                    <input type="date" v-model="form.date">
                </div>
                <div class="input-group">
                    <label>🔄 业务类型</label>
                    <div class="radio-group">
                        <label><input type="radio" value="borrow" v-model="form.lendType"> 📤 借出</label>
                        <label><input type="radio" value="return" v-model="form.lendType"> 📥 归还</label>
                    </div>
                </div>
                <div class="input-group" v-if="form.lendType === 'return'">
                    <label>🔁 关联未归还借出记录 (选择后自动匹配店铺)</label>
                    <select v-model="form.linkedBorrowId">
                        <option value="">--选择借出单号--</option>
                        <option v-for="borrow in availableBorrowRecords" :value="borrow.id" :key="borrow.id">
                            [{{ borrow.date }}] {{ borrow.outShop }} → {{ borrow.inShop }} | {{ borrow.productName }} x{{ borrow.quantity }}
                        </option>
                    </select>
                    <div class="info-note" v-if="form.linkedBorrowId">✔ 配对完成后双方记录均不出现在报表中</div>
                </div>
                <div class="input-group" style="flex-direction: row; gap: 8px;">
                    <button @click="addTransfer">✅ 登记借/还</button>
                    <button class="btn-outline" @click="resetForm">重置</button>
                </div>
            </div>
        </div>

        <!-- 调拨记录列表（全部原始记录） -->
        <div class="card">
            <div class="card-header">
                <h2>📋 全部调拨记录 (含已配对)</h2>
                <button class="btn-outline btn-sm" @click="exportAllTransfers">📎 导出全部记录</button>
            </div>
            <div class="filter-bar">
                <input type="month" v-model="filterMonth" style="width: 130px;" placeholder="按月份">
                <button class="btn-outline btn-sm" @click="filterMonth = ''">清除</button>
                <span style="font-size:0.7rem;">共 {{ filteredTransfers.length }} 条 | 🟡借 🟢还 ✅已配对自动隐藏报表</span>
            </div>
            <div class="table-wrapper">
                <table>
                    <thead>
                        <tr><th>类型</th><th>调出</th><th>调入</th><th>类别</th><th>产品编码</th><th>产品</th><th>规格</th><th>数量</th><th>日期</th><th>配对状态</th><th>操作</th></tr>
                    </thead>
                    <tbody>
                        <tr v-for="t in filteredTransfers" :key="t.id">
                            <td><span :class="['badge-cat', t.lendType === 'borrow' ? 'badge-borrow' : 'badge-return']">{{ t.lendType === 'borrow' ? '借出' : '归还' }}</span></td>
                            <td>{{ t.outShop }}</td><td>{{ t.inShop }}</td>
                            <td>{{ t.category }}</td>
                            <td><code>{{ t.productCode || '--' }}</code></td>
                            <td><strong>{{ t.productName }}</strong></td>
                            <td>{{ t.spec }}</td>
                            <td>{{ t.quantity }}</td>
                            <td>{{ t.date }}</td>
                            <td><span v-if="t.pairedFlag" style="color:#2b9348;">✅ 已配对(报表隐藏)</span><span v-else style="color:#dc843a;">⚪ 未配对</span></td>
                            <td><button class="btn-outline btn-sm" @click="editTransfer(t)">✏️</button>
                                <button class="btn-outline btn-sm" @click="deleteTransfer(t.id)" style="color:#b91c1c;">🗑️</button></td>
                        </tr>
                        <tr v-if="filteredTransfers.length === 0"><td colspan="11" style="text-align:center; padding: 24px;">暂无记录</td></tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <!-- 产品库模态框：增加编码 -->
    <div v-if="showProductModal" class="modal-mask" @click.self="showProductModal=false">
        <div class="modal-container">
            <div class="modal-header"><h3>📦 产品清单 (含编码)</h3><button class="close-modal" @click="showProductModal=false">✕</button></div>
            <div style="margin-bottom: 14px; display: flex; gap: 8px; flex-wrap: wrap;">
                <label class="btn-outline btn-sm" style="cursor:pointer;">📂 导入Excel (需含编码)<input type="file" accept=".xlsx, .xls, .csv" @change="importProductExcel" style="display:none;"></label>
                <button class="btn-outline btn-sm" @click="downloadProductTemplate">📄 模板(含编码)</button>
            </div>
            <div style="display: flex; gap:6px; margin-bottom: 14px; flex-wrap:wrap;">
                <select v-model="newProduct.category" style="width:110px;"><option value="">类别</option><option v-for="c in allCategories" :value="c">{{ c }}</option></select>
                <input v-model="newProduct.code" placeholder="产品编码*" style="width:110px;">
                <input v-model="newProduct.name" placeholder="产品名" style="flex:1;">
                <input v-model="newProduct.spec" placeholder="规格" style="flex:1;">
                <button @click="addProductItem">➕添加</button>
            </div>
            <div style="max-height: 45vh; overflow-y: auto;">
                <div v-for="cat in allCategories" :key="cat" style="margin-bottom: 16px;">
                    <h4 style="font-size:0.8rem; background:#f0f4fe; padding: 4px 10px; border-radius: 30px;">{{ cat }}</h4>
                    <div v-for="prod in productsByCategoryFilter(cat)" :key="prod.id" class="product-item">
                        <div><strong>{{ prod.name }}</strong> <span class="badge-cat">{{ prod.code }}</span> <span style="color:#64748b;">{{ prod.spec }}</span></div>
                        <div><button class="btn-outline btn-sm" @click="editProductItem(prod)">编辑</button><button class="btn-outline btn-sm" @click="deleteProductItem(prod.id)" style="margin-left:5px;">删除</button></div>
                    </div>
                    <div v-if="productsByCategoryFilter(cat).length === 0" style="padding:6px; color:#8aa0bc;">暂无</div>
                </div>
            </div>
        </div>
    </div>

    <!-- 门店管理模态框 -->
    <div v-if="showShopModal" class="modal-mask" @click.self="showShopModal=false">
        <div class="modal-container"><div class="modal-header"><h3>🏢 门店管理</h3><button class="close-modal" @click="showShopModal=false">✕</button></div>
        <div style="display: flex; gap: 8px; margin-bottom: 16px;"><input type="text" v-model="newShopName" placeholder="新门店名称"><button @click="addNewShop">➕ 增加</button></div>
        <div><div v-for="shop in shopList" :key="shop" class="shop-item"><span>{{ shop }}</span><button class="btn-outline btn-sm" @click="removeShop(shop)" :disabled="shopList.length <= 1">删除</button></div></div>
        <div class="footer-note">至少保留一家门店，历史调拨记录保留门店名</div></div>
    </div>

    <!-- 报表模态框 (只显示未配对的借/还记录：即未完成闭环的调拨) -->
    <div v-if="showReportModal" class="modal-mask" @click.self="showReportModal=false">
        <div class="modal-container" style="width: 95%; max-width: 1000px;">
            <div class="modal-header"><h3>📊 报表 (仅未配对借还 · 已配对自动隐藏)</h3><button class="close-modal" @click="showReportModal=false">✕</button></div>
            <div class="date-range">
                <div class="input-group"><label>起始日期</label><input type="date" v-model="reportStartDate"></div>
                <div class="input-group"><label>结束日期</label><input type="date" v-model="reportEndDate"></div>
                <button @click="generateReportByDateRange" style="margin-top:22px;">生成报表(未结清)</button>
                <button class="btn-outline" @click="exportDateRangeReportExcel" style="margin-top:22px;">导出Excel</button>
            </div>
            <div v-if="fullReportReady" class="range-summary">📅 范围：{{ reportStartDate || '最早' }} 至 {{ reportEndDate || '最新' }} &nbsp;|&nbsp; 未结清调拨 {{ reportDetailRows.length }} 条</div>
            <div v-if="!fullReportReady" style="padding: 24px; text-align: center;">⬅️ 选择日期范围后点击生成 (已配对记录已过滤)</div>
            <div v-else style="max-height: 50vh; overflow-y: auto;">
                <h4>📋 未抵消调拨明细</h4>
                <div class="table-wrapper"><table><thead><tr><th>类型</th><th>调出</th><th>调入</th><th>类别</th><th>产品编码</th><th>产品</th><th>数量</th><th>日期</th></tr></thead>
                <tbody><tr v-for="(item,idx) in reportDetailRows" :key="idx"><td>{{ item.lendType === 'borrow' ? '借出' : '归还' }}</td><td>{{ item.outShop }}</td><td>{{ item.inShop }}</td><td>{{ item.category }}</td><td>{{ item.productCode }}</td><td>{{ item.productName }}</td><td>{{ item.quantity }}</td><td>{{ item.date }}</td></tr>
                <tr v-if="reportDetailRows.length===0"><td colspan="8">🎉 无未结清调拨，所有借还已闭环</td></tr></tbody></table></div>
                <h4>📊 门店净流量矩阵 (未配对调拨)</h4>
                <div class="table-wrapper"><table><thead><tr><th>调出\调入</th><th v-for="s in shopListForMatrix">{{ s }}</th><th>总调出(未结清)</th></tr></thead>
                <tbody><tr v-for="out in shopListForMatrix" :key="out"><td style="font-weight:600;">{{ out }}</td><td v-for="inp in shopListForMatrix">{{ getMatrixValue(out, inp) || 0 }}</td><td style="background:#eef2ff;">{{ getOutTotalVal(out) }}</td></tr>
                <tr style="background:#f8fafc;"><td>总调入(未结清)</td><td v-for="inp in shopListForMatrix">{{ getInTotalVal(inp) }}</td><td>{{ totalFlowAmount }}</td></tr></tbody></table></div>
            </div>
        </div>
    </div>
    <div class="version-info">✅ 借出+归还配对后自动隐藏报表 | 产品编码唯一追踪 | 本地存储</div>
</div>

<script>
    const { createApp, ref, computed, onMounted } = Vue;
    createApp({
        setup() {
            const allCategories = ['乳制品类', '原料类', '包材类', '糕点类', '冰棒类'];
            const shopList = ref(['农垦店', '东葛店', '农信社店', '佛子岭店', '云景店']);
            const products = ref([]);
            const transfers = ref([]);
            
            // 表单
            const form = ref({
                id: null, outShop: '', inShop: '', category: '', productId: null, productCode: '', spec: '', quantity: 1,
                date: new Date().toISOString().slice(0,10), selectedProductName: '', lendType: 'borrow', linkedBorrowId: ''
            });
            const filterMonth = ref('');
            const showProductModal = ref(false);
            const showShopModal = ref(false);
            const showReportModal = ref(false);
            const reportStartDate = ref('');
            const reportEndDate = ref('');
            const fullReportReady = ref(false);
            const reportDetailRows = ref([]);
            const reportMatrix = ref({});
            const outTotalMap = ref({});
            const inTotalMap = ref({});
            const newProduct = ref({ category: '', name: '', spec: '', code: '' });
            const newShopName = ref('');
            const productKeyword = ref('');
            const showProductDropdown = ref(false);
            
            // 可供选择的未配对借出记录（用于归还时关联）
            const availableBorrowRecords = computed(() => {
                if (!form.value.category || !form.value.productId) return [];
                // 筛选未配对、类型为借出、且产品ID匹配，并且店铺逻辑: 归还时应该由借入方向借出方归还，但方便用户，展示所有未配对借出，选择后自动反转门店
                return transfers.value.filter(t => 
                    t.lendType === 'borrow' && t.pairedFlag !== true && t.productId === form.value.productId
                );
            });
            
            // 监听关联借记录，自动填充门店（归还时调出门店应为原借入店，调入门店应为原借出店）
            const updateShopsByLinkedBorrow = () => {
                if (form.value.lendType === 'return' && form.value.linkedBorrowId) {
                    const borrowRec = transfers.value.find(t => t.id == form.value.linkedBorrowId);
                    if (borrowRec) {
                        form.value.outShop = borrowRec.inShop;
                        form.value.inShop = borrowRec.outShop;
                        if (!form.value.quantity) form.value.quantity = borrowRec.quantity;
                    }
                }
            };
            
            const filteredSearchProducts = computed(() => {
                if (!form.value.category) return [];
                let list = products.value.filter(p => p.category === form.value.category);
                const kw = productKeyword.value.trim().toLowerCase();
                if (kw) list = list.filter(p => p.name.toLowerCase().includes(kw) || (p.code && p.code.toLowerCase().includes(kw)));
                return list;
            });
            const onProductKeywordInput = () => { showProductDropdown.value = true; };
            const selectProduct = (prod) => {
                form.value.productId = prod.id;
                form.value.productCode = prod.code || '';
                form.value.spec = prod.spec;
                form.value.selectedProductName = prod.name;
                productKeyword.value = prod.name + (prod.code ? `(${prod.code})` : '');
                showProductDropdown.value = false;
                if (form.value.category !== prod.category) form.value.category = prod.category;
                // 若归还类型，刷新可用借出列表
            };
            const handleDropdownBlur = () => { setTimeout(() => { showProductDropdown.value = false; }, 200); };
            const onCategoryChange = () => {
                form.value.productId = null;
                form.value.productCode = '';
                form.value.spec = '';
                form.value.selectedProductName = '';
                productKeyword.value = '';
                form.value.linkedBorrowId = '';
                showProductDropdown.value = false;
            };
            
            // 保存数据
            const saveData = () => {
                localStorage.setItem('mobile_shops_v2', JSON.stringify(shopList.value));
                localStorage.setItem('mobile_products_v2', JSON.stringify(products.value));
                localStorage.setItem('mobile_transfers_v2', JSON.stringify(transfers.value));
            };
            const loadData = () => {
                const storedShops = localStorage.getItem('mobile_shops_v2');
                if(storedShops) shopList.value = JSON.parse(storedShops);
                const storedProducts = localStorage.getItem('mobile_products_v2');
                if(storedProducts) products.value = JSON.parse(storedProducts);
                else {
                    products.value = [
                        { id: 1, category: '乳制品类', code: 'MILK01', name: '纯牛奶', spec: '250ml*24盒' },
                        { id: 2, category: '乳制品类', code: 'YOG02', name: '酸奶', spec: '180g*12杯' },
                        { id: 3, category: '原料类', code: 'FLOUR03', name: '高筋面粉', spec: '25kg/袋' },
                        { id: 4, category: '原料类', code: 'BUTTER04', name: '黄油', spec: '10kg/箱' },
                        { id: 5, category: '包材类', code: 'BOX05', name: '纸质打包盒', spec: '500只/箱' },
                        { id: 6, category: '糕点类', code: 'TART06', name: '蛋挞皮', spec: '30个/包' },
                        { id: 7, category: '冰棒类', code: 'ICE07', name: '红豆冰棒', spec: '80g*50支' }
                    ];
                }
                const storedTransfers = localStorage.getItem('mobile_transfers_v2');
                if(storedTransfers) transfers.value = JSON.parse(storedTransfers);
                else transfers.value = [];
                // 兼容旧数据: 无lendType字段默认为borrow；无pairedFlag默认为false；无productCode从产品补全
                transfers.value.forEach(t => {
                    if (!t.lendType) t.lendType = 'borrow';
                    if (t.pairedFlag === undefined) t.pairedFlag = false;
                    if (!t.productCode) {
                        const prod = products.value.find(p => p.id === t.productId);
                        if (prod) t.productCode = prod.code || '';
                    }
                });
                saveData();
            };
            
            // 核心登记逻辑：借/还 + 配对
            const addTransfer = () => {
                let { outShop, inShop, category, productId, quantity, date, id, lendType, linkedBorrowId } = form.value;
                if(!outShop || !inShop || !category || !productId || !quantity || quantity<=0) { alert('请完整填写信息'); return; }
                if(outShop === inShop) { alert('调出/调入不可相同'); return; }
                const prod = products.value.find(p => p.id == productId);
                if(!prod) { alert('产品无效'); return; }
                if(lendType === 'return' && !linkedBorrowId) { alert('归还类型必须选择关联的借出记录'); return; }
                
                const newRec = {
                    id: id || Date.now(), outShop, inShop, category, productId,
                    productName: prod.name, productCode: prod.code || '', spec: prod.spec,
                    quantity: Number(quantity), date, lendType, pairedFlag: false, linkedBorrowId: null
                };
                if(lendType === 'return' && linkedBorrowId) {
                    const borrowRec = transfers.value.find(t => t.id == linkedBorrowId);
                    if(!borrowRec || borrowRec.pairedFlag) { alert('借出记录无效或已配对'); return; }
                    newRec.linkedBorrowId = linkedBorrowId;
                    // 配对双方
                    borrowRec.pairedFlag = true;
                    newRec.pairedFlag = true;
                }
                if(id) {
                    const idx = transfers.value.findIndex(t => t.id === id);
                    if(idx !== -1) transfers.value[idx] = newRec;
                } else {
                    transfers.value.push(newRec);
                }
                saveData();
                resetForm();
                alert(lendType === 'return' ? '归还成功，与原借记录完成配对，报表自动隐藏' : '借出登记成功');
            };
            const resetForm = () => {
                form.value = { id: null, outShop: '', inShop: '', category: '', productId: null, productCode: '', spec: '', quantity: 1, date: new Date().toISOString().slice(0,10), selectedProductName: '', lendType: 'borrow', linkedBorrowId: '' };
                productKeyword.value = '';
                showProductDropdown.value = false;
            };
            const editTransfer = (t) => {
                if(t.pairedFlag) { alert('已配对记录不可编辑，请删除后重新登记'); return; }
                const prodMatch = products.value.find(p => p.id === t.productId);
                form.value = { 
                    id: t.id, outShop: t.outShop, inShop: t.inShop, category: t.category, 
                    productId: t.productId, productCode: t.productCode, spec: t.spec, quantity: t.quantity, 
                    date: t.date, selectedProductName: t.productName, lendType: t.lendType, linkedBorrowId: ''
                };
                productKeyword.value = t.productName;
                if(t.lendType === 'return' && t.linkedBorrowId) form.value.linkedBorrowId = t.linkedBorrowId;
            };
            const deleteTransfer = (id) => {
                const idx = transfers.value.findIndex(t => t.id === id);
                if(idx === -1) return;
                const rec = transfers.value[idx];
                if(rec.pairedFlag) {
                    if(!confirm('该记录已配对，删除会解除配对并可能影响报表逻辑，确定删除吗？')) return;
                    if(rec.lendType === 'borrow' && rec.pairedFlag) {
                        const linkedReturn = transfers.value.find(t => t.linkedBorrowId === rec.id);
                        if(linkedReturn) linkedReturn.pairedFlag = false;
                    } else if(rec.lendType === 'return' && rec.linkedBorrowId) {
                        const borrowRec = transfers.value.find(t => t.id === rec.linkedBorrowId);
                        if(borrowRec) borrowRec.pairedFlag = false;
                    }
                }
                transfers.value.splice(idx,1);
                saveData();
            };
            const filteredTransfers = computed(() => {
                if(!filterMonth.value) return transfers.value;
                return transfers.value.filter(t => t.date.startsWith(filterMonth.value));
            });
            const exportAllTransfers = () => {
                if(!transfers.value.length) return alert('无记录');
                const data = transfers.value.map(t => ({ '类型':t.lendType==='borrow'?'借出':'归还','调出':t.outShop,'调入':t.inShop,'类别':t.category,'编码':t.productCode,'产品':t.productName,'规格':t.spec,'数量':t.quantity,'日期':t.date,'配对状态':t.pairedFlag?'已配对':'未配对' }));
                const ws = XLSX.utils.json_to_sheet(data);
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, '全部借还记录');
                XLSX.writeFile(wb, `借还记录_${new Date().toISOString().slice(0,19)}.xlsx`);
            };
            // 产品库相关
            const importProductExcel = (event) => {
                const file = event.target.files[0];
                if(!file) return;
                const reader = new FileReader();
                reader.onload = (e) => {
                    const data = new Uint8Array(e.target.result);
                    const workbook = XLSX.read(data, { type: 'array' });
                    const sheet = workbook.Sheets[workbook.SheetNames[0]];
                    const rows = XLSX.utils.sheet_to_json(sheet);
                    let newProducts = [];
                    rows.forEach(row => {
                        let cat = row['产品类别'] || row['类别'] || '';
                        let code = row['产品编码'] || row['编码'] || '';
                        let name = row['产品名称'] || row['名称'] || '';
                        let spec = row['规格'] || '';
                        if(cat && name && allCategories.includes(cat)) { newProducts.push({ id: Date.now() + Math.random(), category: cat, code: String(code), name: name.trim(), spec: spec.trim() }); }
                    });
                    if(newProducts.length) products.value.push(...newProducts);
                    saveData();
                    alert(`导入 ${newProducts.length} 个产品 (含编码)`);
                };
                reader.readAsArrayBuffer(file);
                event.target.value = '';
            };
            const downloadProductTemplate = () => {
                const template = [['产品类别','产品编码','产品名称','规格'],['乳制品类','MILK01','纯牛奶','250ml*24盒'],['糕点类','CAKE02','蛋挞皮','30个/包']];
                const ws = XLSX.utils.aoa_to_sheet(template);
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, '模板');
                XLSX.writeFile(wb, '产品模板(含编码).xlsx');
            };
            const productsByCategoryFilter = (cat) => products.value.filter(p => p.category === cat);
            const addProductItem = () => {
                if(!newProduct.value.category || !newProduct.value.name || !newProduct.value.code) { alert('类别、名称、编码必填'); return; }
                if(products.value.some(p=>p.code === newProduct.value.code && p.category === newProduct.value.category)) { alert('编码重复'); return; }
                products.value.push({ id: Date.now(), category: newProduct.value.category, code: newProduct.value.code.trim(), name: newProduct.value.name.trim(), spec: newProduct.value.spec || '' });
                newProduct.value = { category: '', name: '', spec: '', code: '' };
                saveData();
            };
            const editProductItem = (prod) => {
                const newName = prompt('编辑产品名', prod.name);
                if(newName && newName.trim()) prod.name = newName.trim();
                const newCode = prompt('编辑产品编码', prod.code);
                if(newCode && newCode.trim()) prod.code = newCode.trim();
                const newSpec = prompt('编辑规格', prod.spec);
                if(newSpec !== null) prod.spec = newSpec.trim();
                saveData();
            };
            const deleteProductItem = (id) => { products.value = products.value.filter(p => p.id !== id); saveData(); };
            const addNewShop = () => { if(newShopName.value.trim() && !shopList.value.includes(newShopName.value.trim())) { shopList.value.push(newShopName.value.trim()); newShopName.value = ''; saveData(); } else alert('门店已存在或空'); };
            const removeShop = (shop) => { if(shopList.value.length <= 1) { alert('至少保留一个门店'); return; } if(confirm(`删除 ${shop}`)) { shopList.value = shopList.value.filter(s => s !== shop); saveData(); } };
            const shopListForMatrix = computed(() => shopList.value);
            
            // 报表只取未配对的记录 (pairedFlag !== true)
            const generateReportByDateRange = () => {
                let filtered = transfers.value.filter(t => t.pairedFlag !== true);
                if(reportStartDate.value) filtered = filtered.filter(t => t.date >= reportStartDate.value);
                if(reportEndDate.value) filtered = filtered.filter(t => t.date <= reportEndDate.value);
                reportDetailRows.value = filtered.map(t => ({ ...t }));
                let matrix = {}, outTotal = {}, inTotal = {};
                shopList.value.forEach(out => { matrix[out] = {}; outTotal[out]=0; shopList.value.forEach(inp=> matrix[out][inp]=0); });
                shopList.value.forEach(inp=> inTotal[inp]=0);
                filtered.forEach(rec => { const out = rec.outShop, inp = rec.inShop, qty = Number(rec.quantity);
                    if(shopList.value.includes(out) && shopList.value.includes(inp)) { matrix[out][inp] += qty; outTotal[out] += qty; inTotal[inp] += qty; } });
                reportMatrix.value = matrix; outTotalMap.value = outTotal; inTotalMap.value = inTotal;
                fullReportReady.value = true;
            };
            const getMatrixValue = (out, inp) => reportMatrix.value[out]?.[inp] || 0;
            const getOutTotalVal = (out) => outTotalMap.value[out] || 0;
            const getInTotalVal = (inp) => inTotalMap.value[inp] || 0;
            const totalFlowAmount = computed(() => Object.values(outTotalMap.value).reduce((a,b)=>a+b,0));
            const exportDateRangeReportExcel = () => { if(!fullReportReady.value) return alert('生成报表后导出');
                const wb = XLSX.utils.book_new(); XLSX.utils.book_append_sheet(wb, XLSX.utils.json_to_sheet(reportDetailRows.value), '未结清明细');
                const matRows = [['调出\\调入', ...shopList.value, '总调出']];
                shopList.value.forEach(out => { let row = [out]; let sum=0; shopList.value.forEach(inp=>{ let v=getMatrixValue(out,inp); row.push(v); sum+=v; }); row.push(sum); matRows.push(row); });
                const inRow = ['总调入']; shopList.value.forEach(inp=> inRow.push(getInTotalVal(inp))); inRow.push(totalFlowAmount.value); matRows.push(inRow);
                XLSX.utils.book_append_sheet(wb, XLSX.utils.aoa_to_sheet(matRows), '净流量矩阵');
                XLSX.writeFile(wb, `未结清报表_${reportStartDate.value||'开始'}_${reportEndDate.value||'结束'}.xlsx`);
            };
            const openProductManager = () => { showProductModal.value = true; };
            const openShopManager = () => { showShopModal.value = true; };
            const openFullReportModal = () => { showReportModal.value = true; generateReportByDateRange(); };
            
            onMounted(() => { loadData(); });
            return {
                allCategories, shopList, products, transfers, form, filterMonth, showProductModal, showShopModal, showReportModal,
                reportStartDate, reportEndDate, fullReportReady, reportDetailRows, shopListForMatrix, productKeyword, showProductDropdown,
                filteredSearchProducts, onProductKeywordInput, selectProduct, handleDropdownBlur, onCategoryChange,
                addTransfer, resetForm, editTransfer, deleteTransfer, filteredTransfers, exportAllTransfers,
                importProductExcel, downloadProductTemplate, productsByCategoryFilter, addProductItem, editProductItem, deleteProductItem,
                newProduct, newShopName, addNewShop, removeShop, openProductManager, openShopManager, openFullReportModal,
                generateReportByDateRange, getMatrixValue, getOutTotalVal, getInTotalVal, totalFlowAmount, exportDateRangeReportExcel,
                availableBorrowRecords
            };
        }
    }).mount('#app');
</script>
</body>
</html>
```
