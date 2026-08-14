const bookmarkletCode = `javascript:(function(){fetch('https://weebcentral.com/users/me/subscriptions/data?batchSize=10&maxBatches=50').then(r=>r.text()).then(html=>{const parser=new DOMParser();const doc=parser.parseFromString(html,'text/html');const titles=Array.from(doc.querySelectorAll('article.bg-base-300 h2')).map(el=>el.textContent.trim());const modal=document.createElement('div');modal.style.cssText='position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);background:white;padding:20px;border-radius:8px;box-shadow:0 4px 6px rgba(0,0,0,0.1);z-index:10000;max-width:500px;max-height:80vh;overflow-y:auto;font-family:Arial,sans-serif';const title=document.createElement('h2');title.textContent='Your Manga Subscriptions';title.style.margin='0 0 15px 0';modal.appendChild(title);const list=document.createElement('ul');list.style.cssText='margin:0;padding-left:20px';titles.forEach(t=>{const li=document.createElement('li');li.textContent=t;li.style.cssText='margin-bottom:8px;color:#333';list.appendChild(li)});modal.appendChild(list);const closeBtn=document.createElement('button');closeBtn.textContent='Close';closeBtn.style.cssText='margin-top:15px;padding:8px 16px;background:#007bff;color:white;border:none;border-radius:4px;cursor:pointer';closeBtn.onclick=()=>modal.remove();modal.appendChild(closeBtn);document.body.appendChild(modal)}).catch(err=>alert('Error: '+err.message))})();`;

const copyBtn = document.getElementById('copyBtn');

function copyAndGo() {
  navigator.clipboard.writeText(bookmarkletCode).then(() => {
    copyBtn.textContent = 'Copied! Redirecting...';
    copyBtn.disabled = true;
    setTimeout(() => {
      window.location.href = 'https://weebcentral.com/users/me/subscriptions';
    }, 2000);
  }).catch(() => {
    copyBtn.textContent = 'Failed to copy';
    copyBtn.style.background = '#dc2626';
    setTimeout(() => {
      copyBtn.textContent = 'Copy & Open';
      copyBtn.style.background = '';
    }, 3000);
  });
}

document.addEventListener('DOMContentLoaded', () => {
  copyBtn.addEventListener('click', copyAndGo);
});

window.copyAndGo = copyAndGo;
