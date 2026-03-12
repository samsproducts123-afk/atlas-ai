const CACHE_NAME = 'atlas-v1';
const ASSETS = [
  '/atlas-ai/app.html',
  '/atlas-ai/manifest.json',
  '/atlas-ai/icon-192.png',
  '/atlas-ai/icon-512.png'
];

self.addEventListener('install', e => {
  e.waitUntil(caches.open(CACHE_NAME).then(c => c.addAll(ASSETS)));
  self.skipWaiting();
});

self.addEventListener('activate', e => {
  e.waitUntil(caches.keys().then(keys => 
    Promise.all(keys.filter(k => k !== CACHE_NAME).map(k => caches.delete(k)))
  ));
});

self.addEventListener('fetch', e => {
  if (e.request.url.includes('/v1/chat/completions')) return;
  e.respondWith(
    caches.match(e.request).then(r => r || fetch(e.request))
  );
});
