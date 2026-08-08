# Weebcentral Exporter (Console)

A tool to load and extract subscriptions from Weebcentra

## What It Does

Extracts all titles from your Weebcentral subscriptions or profile and exports them. 

## Usage

### Console 
1. Open your browser console (F12 → Console Tab or Right Click → Inspect Element → Console Tab)
2. Paste the code and press Enter
3. Click the green button that appears → titles exported!

## Supported Pages

- `/users/me/subscriptions` — extracts from your subscription list
- `/users/me/profiles` — extracts from your profile manga grid

## Features

- ✓ Automatic subscription loading and exporting on the subscription pages
- ✓ Works in any modern browser
- ✓ No dependencies
- ✓ No installations required

## License

MIT

---

Made for WeebCentral users who want a quick way to manage and export their subscriptions.

```javascript
(async function(){let targetUrl=window.location.href;let isSubscriptionPage=targetUrl.includes('/subscriptions');let isProfilePage=targetUrl.includes('/profiles');if(!isSubscriptionPage&&!isProfilePage){let container=document.createElement('div');container.style.position='fixed';container.style.top='50%';container.style.left='50%';container.style.transform='translate(-50%, -50%)';container.style.zIndex='99999';container.style.backgroundColor='white';container.style.padding='30px';container.style.borderRadius='8px';container.style.boxShadow='0 4px 6px rgba(0,0,0,0.3)';container.style.textAlign='center';container.innerHTML='<p style="margin: 0 0 20px 0; font-size: 18px;">You are not on the subscriptions or profiles page.</p>';let subBtn=document.createElement('button');subBtn.textContent='Go to Subscriptions Page';subBtn.style.padding='10px 20px';subBtn.style.marginRight='10px';subBtn.style.backgroundColor='#4CAF50';subBtn.style.color='white';subBtn.style.border='none';subBtn.style.borderRadius='4px';subBtn.style.cursor='pointer';subBtn.onclick=()=>window.location.href='https://weebcentral.com/users/me/subscriptions';let profileBtn=document.createElement('button');profileBtn.textContent='Go to Profiles Page';profileBtn.style.padding='10px 20px';profileBtn.style.backgroundColor='#2196F3';profileBtn.style.color='white';profileBtn.style.border='none';profileBtn.style.borderRadius='4px';profileBtn.style.cursor='pointer';profileBtn.onclick=()=>window.location.href='https://weebcentral.com/users/me/profiles';container.appendChild(subBtn);container.appendChild(profileBtn);document.body.appendChild(container);return}if(isSubscriptionPage){let clickCount=0;while(true){let viewMoreBtn=document.querySelector('button[hx-get][hx-swap]');if(viewMoreBtn&&viewMoreBtn.textContent.includes('View More')){viewMoreBtn.click();clickCount++;console.log('Clicked View More '+clickCount+'...');await new Promise(resolve=>setTimeout(resolve,1000))}else{console.log('All subscriptions loaded!');break}}}let titles=Array.from(document.querySelectorAll('article.bg-base-300 h2')).map(el=>el.textContent.trim()).filter(title=>title.length>0);if(titles.length===0){let profileSection=document.querySelector('section.grid.grid-cols-2');if(profileSection){titles=Array.from(profileSection.querySelectorAll('img[alt]')).map(el=>el.getAttribute('alt').replace(/\s+cover$/i,'')).filter(title=>title.length>0)}}console.log('Found '+titles.length+' manga!');console.log(titles.join('\n'));let btn=document.createElement('button');btn.textContent='Copy to Clipboard';btn.style.position='fixed';btn.style.top='10px';btn.style.right='10px';btn.style.zIndex='99999';btn.style.padding='10px 15px';btn.style.backgroundColor='#4CAF50';btn.style.color='white';btn.style.border='none';btn.style.borderRadius='4px';btn.style.cursor='pointer';btn.onclick=()=>{navigator.clipboard.writeText(titles.join('\n')).then(()=>{alert('Copied '+titles.length+' titles to clipboard!');btn.remove()})};document.body.appendChild(btn)})();
