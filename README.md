<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Uphar — Owner Dashboard</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,600;0,700&family=Jost:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --navy:#16233F; --navy-2:#223458; --navy-soft:#3B4A6B;
    --gold:#C9A15D; --gold-light:#E4C98A; --gold-deep:#A9803E;
    --cream:#FBF3E7; --cream-2:#F3E8D8; --white:#FFFDFA; --ink:#2A2A28;
    --line:rgba(22,35,63,0.12); --shadow:0 20px 40px -20px rgba(22,35,63,0.25);
  }
  *{box-sizing:border-box;}
  body{margin:0;background:var(--cream);color:var(--ink);font-family:'Jost',sans-serif;}
  h1,h2,h3{font-family:'Playfair Display',serif;color:var(--navy);margin:0;}
  button{font-family:'Jost',sans-serif;cursor:pointer;}
  img{max-width:100%;display:block;}
  .wrap{max-width:980px;margin:0 auto;padding:40px 24px 80px;}
  .login-shell{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:20px;}
  .login-card{background:var(--white);border-radius:20px;box-shadow:var(--shadow);padding:40px;max-width:380px;width:100%;text-align:center;}
  .login-card h1{font-size:26px;margin-bottom:6px;}
  .login-card p{color:var(--navy-soft);font-size:13px;margin-bottom:24px;}
  .field{margin-bottom:14px;text-align:left;}
  .field label{display:block;font-size:12px;letter-spacing:.04em;text-transform:uppercase;color:var(--navy-soft);margin-bottom:6px;}
  .field input,.field select,.field textarea{width:100%;padding:11px 13px;border-radius:10px;border:1px solid var(--line);font-size:14px;background:var(--cream);color:var(--ink);}
  .field input:focus{outline:2px solid var(--gold);outline-offset:1px;}
  .btn-primary{width:100%;background:var(--navy);color:#fff;padding:13px;border-radius:30px;border:none;font-size:14px;margin-top:6px;transition:.2s;}
  .btn-primary:hover{background:var(--gold-deep);}
  .form-error{color:#a05050;font-size:12px;margin-top:8px;}
  header{display:flex;justify-content:space-between;align-items:center;margin-bottom:30px;flex-wrap:wrap;gap:12px;}
  .logout-btn{border:1px solid var(--navy);background:transparent;color:var(--navy);padding:9px 18px;border-radius:30px;font-size:13px;}
  .logout-btn:hover{background:var(--navy);color:#fff;}
  .tabs{display:flex;gap:8px;margin-bottom:24px;border-bottom:1px solid var(--line);}
  .tab{padding:10px 4px;font-size:14px;color:var(--navy-soft);border:none;background:none;border-bottom:2px solid transparent;margin-right:20px;}
  .tab.active{color:var(--navy);border-color:var(--gold-deep);font-weight:500;}
  .add-product-form{background:var(--white);border:1px solid var(--line);border-radius:16px;padding:22px;margin-bottom:26px;}
  .field-row{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
  @media (max-width:520px){ .field-row{grid-template-columns:1fr;} }
  .admin-product-row{display:flex;gap:14px;align-items:center;padding:14px 0;border-bottom:1px solid var(--line);flex-wrap:wrap;}
  .admin-product-row img{width:56px;height:56px;object-fit:cover;border-radius:10px;flex:none;}
  .api-name{font-family:'Playfair Display',serif;font-size:16px;color:var(--navy);}
  .api-meta{font-size:12px;color:var(--navy-soft);margin-top:2px;}
  .pill{display:inline-block;font-size:10px;padding:3px 9px;border-radius:20px;margin-left:6px;}
  .pill.in{background:#e5f1e6;color:#2f6b34;}
  .pill.out{background:#f6e4e0;color:#a05050;}
  .mini-btn{font-size:12px;padding:7px 12px;border-radius:8px;border:1px solid var(--line);background:#fff;margin-left:8px;margin-top:6px;}
  .mini-btn:hover{border-color:var(--gold-deep);color:var(--gold-deep);}
  .mini-btn.danger:hover{border-color:#a05050;color:#a05050;}
  .order-card{border:1px solid var(--line);border-radius:14px;padding:16px 18px;margin-bottom:14px;background:var(--white);}
  .order-card .oc-head{display:flex;justify-content:space-between;font-size:13px;color:var(--navy-soft);margin-bottom:8px;flex-wrap:wrap;gap:6px;}
  .oc-id{font-family:'Playfair Display',serif;color:var(--navy);font-size:15px;}
  .oc-addr{font-size:13px;line-height:1.6;color:var(--navy-2);background:var(--cream);border-radius:10px;padding:10px 12px;margin-top:8px;}
  .order-card ul{margin:8px 0 0;padding-left:18px;font-size:13px;}
  .fine{font-size:12px;color:var(--navy-soft);margin-top:20px;line-height:1.7;max-width:640px;}
  .empty{color:var(--navy-soft);font-size:14px;padding:20px 0;}
  .btn-primary.small{width:auto;padding:11px 20px;}
</style>
</head>
<body>

<div id="loginView" class="login-shell">
  <div class="login-card">
    <h1>Owner Login</h1>
    <p>Sign in to manage your Uphar store.</p>
    <div class="field"><label>Email</label><input id="li_email" type="email" placeholder="you@email.com"></div>
    <div class="field"><label>Password</label><input id="li_pass" type="password" placeholder="••••••••"></div>
    <button class="btn-primary" onclick="doLogin()">Sign In</button>
    <div class="form-error" id="loginError"></div>
  </div>
</div>

<div id="dashboardView" class="wrap" style="display:none;">
  <header>
    <h1>Store Dashboard</h1>
    <button class="logout-btn" onclick="doLogout()">Sign Out</button>
  </header>

  <div class="tabs">
    <button class="tab active" data-tab="products" onclick="switchTab('products')">Products</button>
    <button class="tab" data-tab="orders" onclick="switchTab('orders')">Orders</button>
  </div>

  <div id="productsTab">
    <div class="add-product-form">
      <h3 id="formTitle" style="font-size:18px;margin-bottom:14px;">Add New Product</h3>
      <div class="field-row">
        <div class="field"><label>Product Name</label><input id="np_name" placeholder="e.g. Rose Bloom Bouquet"></div>
        <div class="field"><label>Category</label>
          <select id="np_cat"><option>Bouquets</option><option>Wall Art</option><option>Gift Boxes</option><option>Custom</option></select>
        </div>
      </div>
      <div class="field-row">
        <div class="field"><label>Price (₹)</label><input id="np_price" type="number" min="0" placeholder="1299"></div>
        <div class="field"><label>Discount %</label><input id="np_discount" type="number" min="0" max="90" placeholder="0"></div>
      </div>
      <div class="field"><label>Image URL</label><input id="np_image" placeholder="https://..."></div>
      <div class="field"><label>Short Description</label><input id="np_desc" placeholder="One line about this piece"></div>
      <button class="btn-primary small" id="formSaveBtn" onclick="addProduct()">Add Product</button>
      <button class="mini-btn" id="formCancelBtn" style="display:none;" onclick="cancelEdit()">Cancel</button>
    </div>
    <div id="productList"></div>
  </div>

  <div id="ordersTab" style="display:none;">
    <div id="orderList"></div>
  </div>

  <p class="fine">Courier integration: each order below includes the full delivery address. To auto-schedule pickups with Ecom Express, Shiprocket, or similar, you'll connect their Pickup API using your registered seller credentials — that call has to be made from a small backend function (not this page directly), since it needs a private API key. Happy to build that once you have a courier account.</p>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
import {
  getAuth, signInWithEmailAndPassword, onAuthStateChanged, signOut
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";
import {
  getFirestore, collection, getDocs, doc, setDoc, updateDoc, deleteDoc
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "AIzaSyCbbBe6yql_4i34BwBxt5rmRclzHaKEQw0",
  authDomain: "uphar-store-8b3eb.firebaseapp.com",
  projectId: "uphar-store-8b3eb",
  storageBucket: "uphar-store-8b3eb.firebasestorage.app",
  messagingSenderId: "300507168746",
  appId: "1:300507168746:web:85ebc47d1385bbc37f7c93"
};
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

let PRODUCTS = [];
let ORDERS = [];

window.doLogin = async function(){
  const email = document.getElementById('li_email').value.trim();
  const pass = document.getElementById('li_pass').value;
  document.getElementById('loginError').textContent = '';
  try{
    await signInWithEmailAndPassword(auth, email, pass);
  }catch(err){
    document.getElementById('loginError').textContent = 'Incorrect email or password.';
  }
};
window.doLogout = function(){ signOut(auth); };

onAuthStateChanged(auth, (user) => {
  if(user){
    document.getElementById('loginView').style.display = 'none';
    document.getElementById('dashboardView').style.display = 'block';
    loadProducts();
    loadOrders();
  } else {
    document.getElementById('loginView').style.display = 'flex';
    document.getElementById('dashboardView').style.display = 'none';
  }
});

window.switchTab = function(tab){
  document.getElementById('productsTab').style.display = tab==='products' ? 'block' : 'none';
  document.getElementById('ordersTab').style.display = tab==='orders' ? 'block' : 'none';
  document.querySelectorAll('.tab').forEach(b=>b.classList.toggle('active', b.dataset.tab===tab));
};

function money(n){ return '₹' + Number(n).toLocaleString('en-IN'); }

async function loadProducts(){
  const snap = await getDocs(collection(db, 'products'));
  PRODUCTS = snap.docs.map(d => ({ id: d.id, ...d.data() }));
  renderProducts();
}
function renderProducts(){
  const el = document.getElementById('productList');
  if(PRODUCTS.length===0){ el.innerHTML = '<p class="empty">No products yet. Add your first one above.</p>'; return; }
  el.innerHTML = PRODUCTS.map(p=>`
    <div class="admin-product-row">
      <img src="${p.image}" alt="${p.name}">
      <div style="flex:1;min-width:180px;">
        <div class="api-name">${p.name}</div>
        <div class="api-meta">${p.category} · ${money(p.price)} ${p.discount>0?`(${p.discount}% off)`:''}
          <span class="pill ${p.stock?'in':'out'}">${p.stock?'In Stock':'Out of Stock'}</span>
        </div>
      </div>
      <div>
        <button class="mini-btn" onclick="startEdit('${p.id}')">Edit</button>
        <button class="mini-btn" onclick="toggleStock('${p.id}')">${p.stock?'Mark Out of Stock':'Mark In Stock'}</button>
        <button class="mini-btn" onclick="editDiscount('${p.id}')">Set Discount</button>
        <button class="mini-btn" onclick="editPrice('${p.id}')">Edit Price</button>
        <button class="mini-btn danger" onclick="deleteProduct('${p.id}')">Delete</button>
      </div>
    </div>
  `).join('');
}
window.toggleStock = async function(id){
  const p = PRODUCTS.find(x=>x.id===id);
  await updateDoc(doc(db,'products',id), { stock: !p.stock });
  await loadProducts();
};
window.editDiscount = async function(id){
  const p = PRODUCTS.find(x=>x.id===id);
  const v = prompt('Set discount % for "'+p.name+'" (0 for none):', p.discount||0);
  if(v===null) return;
  await updateDoc(doc(db,'products',id), { discount: Math.max(0, Math.min(90, parseInt(v)||0)) });
  await loadProducts();
};
window.editPrice = async function(id){
  const p = PRODUCTS.find(x=>x.id===id);
  const v = prompt('Set new price (₹) for "'+p.name+'":', p.price);
  if(v===null) return;
  await updateDoc(doc(db,'products',id), { price: Math.max(0, parseInt(v)||p.price) });
  await loadProducts();
};
window.deleteProduct = async function(id){
  if(!confirm('Delete this product permanently?')) return;
  await deleteDoc(doc(db,'products',id));
  await loadProducts();
};
let editingId = null;

window.startEdit = function(id){
  const p = PRODUCTS.find(x=>x.id===id);
  if(!p) return;
  editingId = id;
  document.getElementById('np_name').value = p.name;
  document.getElementById('np_cat').value = p.category;
  document.getElementById('np_price').value = p.price;
  document.getElementById('np_discount').value = p.discount || 0;
  document.getElementById('np_image').value = p.image;
  document.getElementById('np_desc').value = p.desc || '';
  document.getElementById('formTitle').textContent = 'Editing: ' + p.name;
  document.getElementById('formSaveBtn').textContent = 'Save Changes';
  document.getElementById('formCancelBtn').style.display = 'inline-block';
  document.querySelector('.add-product-form').scrollIntoView({behavior:'smooth'});
};
window.cancelEdit = function(){
  editingId = null;
  ['np_name','np_price','np_discount','np_image','np_desc'].forEach(fid=>document.getElementById(fid).value='');
  document.getElementById('formTitle').textContent = 'Add New Product';
  document.getElementById('formSaveBtn').textContent = 'Add Product';
  document.getElementById('formCancelBtn').style.display = 'none';
};
window.addProduct = async function(){
  const name = document.getElementById('np_name').value.trim();
  const price = parseInt(document.getElementById('np_price').value)||0;
  if(!name || !price){ alert('Enter a name and price'); return; }
  const product = {
    name,
    category: document.getElementById('np_cat').value,
    price,
    discount: parseInt(document.getElementById('np_discount').value)||0,
    stock: editingId ? PRODUCTS.find(x=>x.id===editingId).stock : true,
    image: document.getElementById('np_image').value.trim() || 'https://images.unsplash.com/photo-1487070183336-b863922373d4?w=500&q=80',
    desc: document.getElementById('np_desc').value.trim()
  };
  const id = editingId || ('p' + Date.now());
  await setDoc(doc(db,'products', id), product);
  cancelEdit();
  await loadProducts();
};

async function loadOrders(){
  const snap = await getDocs(collection(db, 'orders'));
  ORDERS = snap.docs.map(d => ({ docId: d.id, ...d.data() }));
  ORDERS.sort((a,b) => new Date(b.date) - new Date(a.date));
  renderOrders();
}
function renderOrders(){
  const el = document.getElementById('orderList');
  if(ORDERS.length===0){ el.innerHTML = '<p class="empty">No orders yet.</p>'; return; }
  el.innerHTML = ORDERS.map(o=>`
    <div class="order-card">
      <div class="oc-head"><span class="oc-id">${o.orderId}</span><span>${new Date(o.date).toLocaleString()}</span></div>
      <div>${o.customer.name} · ${o.customer.phone}</div>
      <ul>${o.items.map(i=>`<li>${i.name} × ${i.qty} — ${money(i.price*i.qty)}</li>`).join('')}</ul>
      <div style="margin-top:6px;font-weight:500;">Total: ${money(o.total)} · ${o.customer.payment}</div>
      <div class="oc-addr">${o.customer.address}, ${o.customer.city}, ${o.customer.state} — ${o.customer.pincode}${o.customer.note?`<br><em>Note: ${o.customer.note}</em>`:''}</div>
      <div class="field" style="max-width:220px;margin-top:10px;">
        <select onchange="updateStatus('${o.docId}', this.value)">
          ${['Placed','Packed','Shipped','Out for Delivery','Delivered','Cancelled'].map(s=>`<option ${s===o.status?'selected':''}>${s}</option>`).join('')}
        </select>
      </div>
    </div>
  `).join('');
}
window.updateStatus = async function(docId, status){
  await updateDoc(doc(db,'orders',docId), { status });
  await loadOrders();
};
</script>
</body>
</html>
