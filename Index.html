<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hoppborg Validator - EN 14960-1:2019</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { font-family: system-ui, -apple-system, sans-serif; }
    </style>
</head>
<body class="bg-gray-50">
    <div id="app" class="max-w-4xl mx-auto p-4"></div>

    <script>
        const app = {
            lang: 'sv',
            data: {
                length: '', width: '', height: '', platformHeight: '', wallHeight: '',
                type: '', productId: '', idVisible: '', hasRopes: '', anchorPoints: '',
                anchorAngle: '', hasNetting: '', nettingMesh: '', nettingCorners: '',
                blowerCount: '', blowerPower: '', blowerTube: '', maxUsers: '', maxUserHeight: ''
            },
            result: null,
            cameraActive: false,
            stream: null
        };

        function calc() {
            const L = parseFloat(app.data.length) || 0;
            const W = parseFloat(app.data.width) || 0;
            const H = parseFloat(app.data.height) || 0;
            
            if (!L || !W || !H) return null;

            const sides = [
                { name: 'Långsida 1', len: L, area: L * H },
                { name: 'Långsida 2', len: L, area: L * H },
                { name: 'Kortsida 1', len: W, area: W * H },
                { name: 'Kortsida 2', len: W, area: W * H }
            ];

            const anchors = sides.map(s => {
                const F = 0.5 * 1.5 * 1.24 * 11.1 * 11.1 * s.area;
                const n = F / 1600;
                let need = Math.ceil(n);
                if (n % 1 > 0.6) need += 1;
                need = Math.max(need, 2);
                return { ...s, need, space: (s.len / need).toFixed(2) };
            });

            const total = anchors.reduce((sum, a) => sum + a.need, 0);
            const minAnchors = Math.max(6, total);
            const area = Math.max(0, (L - 0.6) * (W - 0.6));
            const maxU = Math.floor(area / 2);

            return { anchors, minAnchors, area: area.toFixed(2), maxU };
        }

        function validate() {
            const c = calc();
            if (!c) return;

            const issues = [];
            const passes = [];

            if (!app.data.productId) {
                issues.push({ cat: 'Märkning', msg: 'Produkt-ID saknas', ref: '8' });
            }

            if (app.data.idVisible === 'no') {
                issues.push({ cat: 'Märkning', msg: 'ID ej synligt', ref: '8' });
            }

            if (app.data.hasRopes === 'yes') {
                issues.push({ cat: 'Säkerhet', msg: 'REP FÖRBJUDET - Strypningsrisk!', ref: '4.1.4' });
            }

            const ap = parseInt(app.data.anchorPoints) || 0;
            if (ap > 0 && ap < c.minAnchors) {
                issues.push({ cat: 'Fästpunkter', msg: `För få: ${ap} st (behöver ${c.minAnchors} st)`, ref: 'Annex A' });
            } else if (ap >= c.minAnchors) {
                passes.push('Fästpunkter antal OK');
            }

            const angle = parseInt(app.data.anchorAngle) || 0;
            if (angle > 0 && (angle < 30 || angle > 45)) {
                issues.push({ cat: 'Fästpunkter', msg: `Fel vinkel: ${angle}° (ska vara 30-45°)`, ref: '4.2.1' });
            } else if (angle >= 30 && angle <= 45) {
                passes.push(`Förankringsvinkel OK (${angle}°)`);
            }

            if (app.data.hasNetting === 'yes') {
                const mesh = parseFloat(app.data.nettingMesh) || 0;
                if (mesh > 8) {
                    issues.push({ cat: 'Nät', msg: `Maskor ${mesh}mm > 8mm`, ref: '4.1.3' });
                }
                if (app.data.nettingCorners === 'no') {
                    issues.push({ cat: 'Nät', msg: 'Når ej hörn', ref: '4.2.9' });
                }
            }

            const bt = parseFloat(app.data.blowerTube) || 0;
            if (bt > 0 && bt < 1.2) {
                issues.push({ cat: 'Inblås', msg: `Rör ${bt}m < 1.2m`, ref: '4.2.4' });
            }

            app.result = { calc: c, issues, passes, ok: issues.length === 0 };
            
            // Spara till localStorage
            localStorage.setItem('hoppborg_validation', JSON.stringify(app.result));
            localStorage.setItem('hoppborg_data', JSON.stringify(app.data));
            
            render();
        }

        async function startCamera() {
            try {
                app.stream = await navigator.mediaDevices.getUserMedia({ 
                    video: { facingMode: 'environment', width: 1280, height: 720 } 
                });
                const video = document.getElementById('cameraVideo');
                if (video) {
                    video.srcObject = app.stream;
                }
                app.cameraActive = true;
                render();
            } catch (err) {
                alert('Kunde inte starta kamera: ' + err.message);
            }
        }

        function stopCamera() {
            if (app.stream) {
                app.stream.getTracks().forEach(track => track.stop());
                app.stream = null;
            }
            app.cameraActive = false;
            render();
        }

        function render() {
            const container = document.getElementById('app');
            container.innerHTML = `
                <div class="bg-gradient-to-r from-blue-600 to-blue-800 text-white rounded-lg shadow-lg p-6 mb-6">
                    <div class="text-sm opacity-90">EN 14960-1:2019</div>
                    <h1 class="text-3xl font-bold">Hoppborg Validator</h1>
                    <p class="text-sm opacity-90 mt-2">Kontrollera säkerhetskrav enligt standard</p>
                </div>

                <div class="bg-white rounded-lg shadow-lg p-6 mb-6">
                    <h2 class="text-xl font-bold mb-4">Grunduppgifter</h2>
                    
                    <div class="grid grid-cols-3 gap-4 mb-6">
                        <div>
                            <label class="block text-sm font-medium mb-1">Längd (m) *</label>
                            <input type="number" step="0.1" id="length" value="${app.data.length}" 
                                class="w-full p-2 border rounded" placeholder="6.0">
                        </div>
                        <div>
                            <label class="block text-sm font-medium mb-1">Bredd (m) *</label>
                            <input type="number" step="0.1" id="width" value="${app.data.width}"
                                class="w-full p-2 border rounded" placeholder="4.0">
                        </div>
                        <div>
                            <label class="block text-sm font-medium mb-1">Höjd (m) *</label>
                            <input type="number" step="0.1" id="height" value="${app.data.height}"
                                class="w-full p-2 border rounded" placeholder="4.0">
                        </div>
                    </div>

                    <h3 class="text-lg font-semibold mb-3 mt-6">Typ och detaljer</h3>
                    <div class="grid grid-cols-2 gap-4 mb-4">
                        <div>
                            <label class="block text-sm font-medium mb-1">Typ</label>
                            <select id="type" class="w-full p-2 border rounded">
                                <option value="">-- Välj --</option>
                                <option value="open" ${app.data.type === 'open' ? 'selected' : ''}>Öppen</option>
                                <option value="closed" ${app.data.type === 'closed' ? 'selected' : ''}>Sluten</option>
                                <option value="combo" ${app.data.type === 'combo' ? 'selected' : ''}>Kombination</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-medium mb-1">Finns rep *</label>
                            <select id="hasRopes" class="w-full p-2 border rounded">
                                <option value="">-- Välj --</option>
                                <option value="no" ${app.data.hasRopes === 'no' ? 'selected' : ''}>Nej ✓</option>
                                <option value="yes" ${app.data.hasRopes === 'yes' ? 'selected' : ''}>Ja ⚠️</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-medium mb-1">Har nät</label>
                            <select id="hasNetting" class="w-full p-2 border rounded" onchange="render()">
                                <option value="">-- Välj --</option>
                                <option value="yes" ${app.data.hasNetting === 'yes' ? 'selected' : ''}>Ja</option>
                                <option value="no" ${app.data.hasNetting === 'no' ? 'selected' : ''}>Nej</option>
                            </select>
                        </div>
                        ${app.data.hasNetting === 'yes' ? `
                        <div>
                            <label class="block text-sm font-medium mb-1">Maskstorlek (mm)</label>
                            <input type="number" id="nettingMesh" value="${app.data.nettingMesh}"
                                class="w-full p-2 border rounded" placeholder="Max 8">
                        </div>
                        <div>
                            <label class="block text-sm font-medium mb-1">Nät till hörn</label>
                            <select id="nettingCorners" class="w-full p-2 border rounded">
                                <option value="">-- Välj --</option>
                                <option value="yes" ${app.data.nettingCorners === 'yes' ? 'selected' : ''}>Ja</option>
                                <option value="no" ${app.data.nettingCorners === 'no' ? 'selected' : ''}>Nej</option>
                            </select>
                        </div>
                        ` : ''}
                    </div>

                    <h3 class="text-lg font-semibold mb-3 mt-6 pb-2 border-b-2 border-green-600">Lufttryck</h3>
                    <div class="grid grid-cols-2 gap-4 mb-6">
                        <div>
                            <label class="block text-sm font-medium mb-1">Antal fläktar</label>
                            <input type="number" id="blowerCount" value="${app.data.blowerCount}"
                                class="w-full p-2 border rounded" placeholder="1">
                        </div>
                        <div>
                            <label class="block text-sm font-medium mb-1">Effekt per fläkt (W)</label>
                            <input type="number" id="blowerPower" value="${app.data.blowerPower}"
                                class="w-full p-2 border rounded" placeholder="1500">
                        </div>
                    </div>

                    <h3 class="text-lg font-semibold mb-3 mt-6 pb-2 border-b-2 border-blue-600">Förankring</h3>
                    <div class="grid grid-cols-2 gap-4 mb-4">
                        <div>
                            <label class="block text-sm font-medium mb-1">Antal fästpunkter</label>
                            <input type="number" id="anchorPoints" value="${app.data.anchorPoints}"
                                class="w-full p-2 border rounded">
                        </div>
                        <div>
                            <label class="block text-sm font-medium mb-1">Förankringsvinkel (°)</label>
                            <input type="number" id="anchorAngle" value="${app.data.anchorAngle}"
                                class="w-full p-2 border rounded" placeholder="30-45">
                            <p class="text-xs text-gray-500 mt-1">Ska vara 30-45° enligt 4.2.1</p>
                        </div>
                    </div>

                    <button onclick="app.cameraActive ? stopCamera() : startCamera()" 
                        class="w-full flex items-center justify-center gap-2 py-3 rounded-lg font-medium mb-4 ${
                            app.cameraActive 
                                ? 'bg-red-600 hover:bg-red-700 text-white' 
                                : 'bg-green-600 hover:bg-green-700 text-white'
                        }">
                        📷 ${app.cameraActive ? 'Stäng kamera' : 'Öppna kamera för vinkelmätning'}
                    </button>

                    ${app.cameraActive ? `
                    <div class="mb-6 relative bg-black rounded-lg overflow-hidden">
                        <video id="cameraVideo" autoplay playsinline class="w-full"></video>
                        <svg class="absolute inset-0 w-full h-full pointer-events-none" viewBox="0 0 100 100" preserveAspectRatio="none">
                            <line x1="0" y1="80" x2="100" y2="80" stroke="#22c55e" stroke-width="0.5" stroke-dasharray="2,2" />
                            <text x="2" y="78" fill="#22c55e" font-size="3">MARK</text>
                            <line x1="50" y1="80" x2="85" y2="60" stroke="#fbbf24" stroke-width="0.8" />
                            <text x="70" y="58" fill="#fbbf24" font-size="4" font-weight="bold">30°</text>
                            <line x1="50" y1="80" x2="80" y2="50" stroke="#ef4444" stroke-width="0.8" />
                            <text x="65" y="48" fill="#ef4444" font-size="4" font-weight="bold">45°</text>
                            <path d="M 50 80 L 85 60 L 80 50 Z" fill="#22c55e" opacity="0.2" />
                            <circle cx="50" cy="80" r="2" fill="#22c55e" />
                            <text x="50" y="88" fill="#22c55e" font-size="3" text-anchor="middle">Fästpunkt</text>
                            <rect x="2" y="2" width="40" height="18" fill="black" opacity="0.7" rx="2" />
                            <text x="4" y="8" fill="white" font-size="3.5" font-weight="bold">RIKTA IN LINAN</text>
                            <text x="4" y="13" fill="#22c55e" font-size="2.5">✓ Grön zon = OK</text>
                            <text x="4" y="17" fill="#fbbf24" font-size="2.5">⚠ Gul/Röd = Ej OK</text>
                        </svg>
                        <div class="absolute bottom-4 left-0 right-0 text-center">
                            <div class="inline-block bg-black/70 text-white px-4 py-2 rounded-lg text-sm">
                                <div class="font-bold mb-1">Rikta in förankringslinan i bilden</div>
                                <div class="text-xs">Linan ska gå från fästpunkten och ligga mellan de två linjerna</div>
                            </div>
                        </div>
                    </div>
                    ` : ''}

                    <h3 class="text-lg font-semibold mb-3 mt-6 pb-2 border-b-2 border-purple-600">Märkning & Användare</h3>
                    <div class="grid grid-cols-2 gap-4 mb-6">
                        <div>
                            <label class="block text-sm font-medium mb-1">Produkt-ID *</label>
                            <input type="text" id="productId" value="${app.data.productId}"
                                class="w-full p-2 border rounded">
                        </div>
                        <div>
                            <label class="block text-sm font-medium mb-1">ID synligt</label>
                            <select id="idVisible" class="w-full p-2 border rounded">
                                <option value="">-- Välj --</option>
                                <option value="yes" ${app.data.idVisible === 'yes' ? 'selected' : ''}>Ja</option>
                                <option value="no" ${app.data.idVisible === 'no' ? 'selected' : ''}>Nej</option>
                            </select>
                        </div>
                    </div>

                    <button onclick="validate()" class="w-full bg-blue-600 text-white py-3 rounded-lg font-medium hover:bg-blue-700">
                        Validera
                    </button>
                </div>

                ${app.result ? `
                <div class="space-y-6">
                    <div class="rounded-lg shadow-lg p-6 border-l-8 ${
                        app.result.ok ? 'bg-green-50 border-green-500' : 'bg-red-50 border-red-500'
                    }">
                        <div class="flex items-center gap-4">
                            <div class="text-4xl">${app.result.ok ? '✓' : '✗'}</div>
                            <div>
                                <h3 class="text-2xl font-bold">${app.result.ok ? 'GODKÄND' : 'UNDERKÄND'}</h3>
                                <p>${app.result.issues.length === 0 ? 'Inga kritiska fel' : `${app.result.issues.length} kritiska fel`}</p>
                            </div>
                        </div>
                    </div>

                    <div class="bg-blue-50 rounded-lg shadow p-6">
                        <h3 class="text-xl font-bold text-blue-900 mb-4">Beräknade krav</h3>
                        <div class="grid grid-cols-2 gap-4">
                            <div class="bg-white p-4 rounded">
                                <div class="text-sm text-gray-600">Fästpunkter totalt</div>
                                <div class="text-2xl font-bold">${app.result.calc.minAnchors} st</div>
                            </div>
                            <div class="bg-white p-4 rounded">
                                <div class="text-sm text-gray-600">Max användare</div>
                                <div class="text-2xl font-bold">~${app.result.calc.maxU} st</div>
                            </div>
                        </div>
                        <div class="mt-4 bg-white p-4 rounded">
                            <div class="text-sm font-semibold mb-2">Per sida:</div>
                            ${app.result.calc.anchors.map(a => `
                                <div class="text-sm flex justify-between py-1 border-b">
                                    <span>${a.name}:</span>
                                    <span>${a.need} st (avstånd: ${a.space}m)</span>
                                </div>
                            `).join('')}
                        </div>
                    </div>

                    ${app.result.issues.length > 0 ? `
                    <div class="bg-white rounded-lg shadow p-6">
                        <h3 class="text-xl font-bold text-red-900 mb-4">Kritiska fel (${app.result.issues.length})</h3>
                        <div class="space-y-3">
                            ${app.result.issues.map(issue => `
                                <div class="border-l-4 border-red-500 bg-red-50 p-4 rounded">
                                    <div class="font-semibold text-red-900">${issue.cat}</div>
                                    <div class="text-sm mt-1">${issue.msg}</div>
                                    <div class="text-xs text-gray-600 mt-1">EN 14960-1:2019, ${issue.ref}</div>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                    ` : ''}

                    ${app.result.passes.length > 0 ? `
                    <div class="bg-green-50 rounded-lg shadow p-6">
                        <h3 class="text-xl font-bold text-green-900 mb-4">Godkänt (${app.result.passes.length})</h3>
                        ${app.result.passes.map(p => `<div class="text-sm text-green-900">✓ ${p}</div>`).join('')}
                    </div>
                    ` : ''}

                    <button onclick="app.result = null; render();" class="w-full bg-gray-600 text-white py-2 rounded-lg hover:bg-gray-700">
                        Ny validering
                    </button>
                </div>
                ` : ''}
            `;

            // Återställ event listeners
            if (app.cameraActive && app.stream) {
                setTimeout(() => {
                    const video = document.getElementById('cameraVideo');
                    if (video && !video.srcObject) {
                        video.srcObject = app.stream;
                    }
                }, 100);
            }

            // Bind inputs
            ['length', 'width', 'height', 'type', 'hasRopes', 'hasNetting', 'nettingMesh', 
             'nettingCorners', 'blowerCount', 'blowerPower', 'anchorPoints', 'anchorAngle',
             'productId', 'idVisible'].forEach(field => {
                const el = document.getElementById(field);
                if (el) {
                    el.addEventListener('change', (e) => {
                        app.data[field] = e.target.value;
                        if (field === 'hasNetting') render();
                    });
                }
            });
        }

        // Load saved data
        const saved = localStorage.getItem('hoppborg_data');
        if (saved) app.data = JSON.parse(saved);

        // Initial render
        render();
    </script>
</body>
</html>
