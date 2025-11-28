// CodePen (JS panel, Babel) için React kodu
function App() {
  const [dB, setDB] = React.useState(200);   // alt çap (mm)
  const [dT, setDT] = React.useState(80);    // üst çap (mm)
  const [h, setH] = React.useState(150);     // yükseklik (mm)
  const [allowance, setAllowance] = React.useState(10); // dikiş payı (mm)

  // Hesaplama: frustum / kesik koni açılımı
  function compute() {
    const rB = dB / 2.0;
    const rT = dT / 2.0;
    // slant height (yan uzunluk)
    const s = Math.hypot(h, rB - rT);
    // pattern radii: outer = s, inner = s * rT / rB  (korunan yay uzunlukları için)
    const rOuter = s;
    const rInner = rOuter * (rT / rB);
    const angleDeg = (360.0 * rB) / rOuter; // sector açısı
    // yay uzunlukları (kontrol amaçlı)
    const outerArc = 2 * Math.PI * rB;
    const innerArc = 2 * Math.PI * rT;
    return { rB, rT, s, rOuter, rInner, angleDeg, outerArc, innerArc };
  }

  const vals = compute();

  // SVG preview: ölçekleme için
  const previewSize = 420;
  // scale so that outer radius fits comfortably: map rOuter to ~ (previewSize/2)*0.85
  const scale = vals.rOuter > 0 ? ((previewSize / 2) * 0.85) / vals.rOuter : 1;
  const cx = previewSize / 2;
  const cy = previewSize / 2;
  const startAngleRad = 0;
  const endAngleRad = (vals.angleDeg * Math.PI) / 180.0;

  // path oluşturucu (scale uygulayarak)
  function sectorPath(rOut, rIn, angleRad, scaleFactor) {
    const largeArc = angleRad > Math.PI ? 1 : 0;
    const x1o = cx + rOut * Math.cos(0) * scaleFactor;
    const y1o = cy + rOut * Math.sin(0) * scaleFactor;
    const x2o = cx + rOut * Math.cos(angleRad) * scaleFactor;
    const y2o = cy + rOut * Math.sin(angleRad) * scaleFactor;

    const x2i = cx + rIn * Math.cos(angleRad) * scaleFactor;
    const y2i = cy + rIn * Math.sin(angleRad) * scaleFactor;
    const x1i = cx + rIn * Math.cos(0) * scaleFactor;
    const y1i = cy + rIn * Math.sin(0) * scaleFactor;

    return `
      M ${x1o} ${y1o}
      A ${rOut*scaleFactor} ${rOut*scaleFactor} 0 ${largeArc} 1 ${x2o} ${y2o}
      L ${x2i} ${y2i}
      A ${rIn*scaleFactor} ${rIn*scaleFactor} 0 ${largeArc} 0 ${x1i} ${y1i}
      Z
    `;
  }

  // seam rectangle: "kapanma çizgisi" boyunca (angle = 0) innerStart->outerStart,
  // normal outward direction = unit vector perpendicular to that edge.
  // For startAngle=0 radial vector points +x; a perpendicular outward (toward +y) = (0,1).
  function seamRectPoints(rOut, rIn, allowanceMm, scaleFactor) {
    // points in preview coords
    const ox = cx + rOut * scaleFactor;
    const oy = cy + 0;
    const ix = cx + rIn * scaleFactor;
    const iy = cy + 0;
    // outward normal (unit) in preview coords: for angle 0 => (0, -1) or (0,1) depending orientation
    // We will choose outward = toward negative Y (up) so seam appears above the arc;
    // either is acceptable; user said position not critical.
    // Choose outward = (0, -1)
    const outwardX = 0;
    const outwardY = -1;
    const adv = allowanceMm * scaleFactor; // allowance in preview units
    const ox2 = ox + outwardX * adv;
    const oy2 = oy + outwardY * adv;
    const ix2 = ix + outwardX * adv;
    const iy2 = iy + outwardY * adv;
    return {
      outerStart: { x: ox, y: oy },
      innerStart: { x: ix, y: iy },
      outerExtended: { x: ox2, y: oy2 },
      innerExtended: { x: ix2, y: iy2 },
    };
  }

  // SVG download: full-scale in mm (viewBox in mm), with seam rectangle added (allowance in mm).
  function downloadSVG() {
    const rOut = vals.rOuter;
    const rIn = vals.rInner;
    const angleDeg = vals.angleDeg;
    const angleRad = (angleDeg * Math.PI) / 180.0;
    const allow = allowance; // mm

    // Compute sector path in mm, center at (rMax, rMax)
    const rMax = rOut + allow + 5; // margin 5 mm
    const cxmm = rMax;
    const cymm = rMax;

    // coordinates
    function ptOn(r, theta) {
      return { x: cxmm + r * Math.cos(theta), y: cymm + r * Math.sin(theta) };
    }

    const o1 = ptOn(rOut, 0);
    const o2 = ptOn(rOut, angleRad);
    const i2 = ptOn(rIn, angleRad);
    const i1 = ptOn(rIn, 0);

    // seam rectangle: extend the edge (i1->o1) outward by allowance parallel to outward normal
    // radial direction at start=0 is +x; outward normal choose -y (upwards)
    const nx = 0;
    const ny = -1;
    const o1_ext = { x: o1.x + nx * allow, y: o1.y + ny * allow };
    const i1_ext = { x: i1.x + nx * allow, y: i1.y + ny * allow };

    // construct path strings
    const largeArc = angleRad > Math.PI ? 1 : 0;
    const sectorPath = [
      `M ${o1.x.toFixed(4)} ${o1.y.toFixed(4)}`,
      `A ${rOut.toFixed(4)} ${rOut.toFixed(4)} 0 ${largeArc} 1 ${o2.x.toFixed(4)} ${o2.y.toFixed(4)}`,
      `L ${i2.x.toFixed(4)} ${i2.y.toFixed(4)}`,
      `A ${rIn.toFixed(4)} ${rIn.toFixed(4)} 0 ${largeArc} 0 ${i1.x.toFixed(4)} ${i1.y.toFixed(4)}`,
      'Z'
    ].join(' ');

    // seam rect polygon points (i1 -> o1 -> o1_ext -> i1_ext)
    const seamPoly = [
      `${i1.x.toFixed(4)},${i1.y.toFixed(4)}`,
      `${o1.x.toFixed(4)},${o1.y.toFixed(4)}`,
      `${o1_ext.x.toFixed(4)},${o1_ext.y.toFixed(4)}`,
      `${i1_ext.x.toFixed(4)},${i1_ext.y.toFixed(4)}`
    ].join(' ');

    const svg = `<?xml version="1.0" encoding="utf-8"?>
<svg xmlns="http://www.w3.org/2000/svg" width="${(rMax*2).toFixed(4)}mm" height="${(rMax*2).toFixed(4)}mm" viewBox="0 0 ${(rMax*2).toFixed(4)} ${(rMax*2).toFixed(4)}">
  <!-- sector (actual cone pattern) -->
  <path d="${sectorPath}" fill="none" stroke="#000" stroke-width="0.5"/>
  <!-- seam rectangle (allowance) -->
  <polygon points="${seamPoly}" fill="none" stroke="red" stroke-width="0.5"/>
  <!-- helper guides (inner and outer arc outlines) -->
  <circle cx="${cxmm.toFixed(4)}" cy="${cymm.toFixed(4)}" r="${rOut.toFixed(4)}" fill="none" stroke="none"/>
</svg>`;

    const blob = new Blob([svg], { type: 'image/svg+xml' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'cone_pattern_with_seam_mm.svg';
    a.click();
    URL.revokeObjectURL(url);
  }

  // preview seam polygon in preview coords
  const seamPts = seamRectPoints(vals.rOuter, vals.rInner, allowance, scale);

  return (
    <div style={{ fontFamily: 'Arial, sans-serif', padding: 18 }}>
      <h3>Koni Açılımı + Kenara Dikiş Payı (kodlanmış davranış)</h3>

      <div style={{ display: 'flex', gap: 12 }}>
        <div style={{ minWidth: 220 }}>
          <label>Alt çap dB (mm):<br/>
            <input type="number" value={dB} onChange={e => setDB(+e.target.value)} /></label><br/>
          <label>Üst çap dT (mm):<br/>
            <input type="number" value={dT} onChange={e => setDT(+e.target.value)} /></label><br/>
          <label>Yükseklik h (mm):<br/>
            <input type="number" value={h} onChange={e => setH(+e.target.value)} /></label><br/>
          <label>Dikiş payı (mm):<br/>
            <input type="number" value={allowance} onChange={e => setAllowance(+e.target.value)} /></label><br/><br/>

          <button onClick={downloadSVG}>SVG indir (tam ölçek, mm)</button>
        </div>

        <div>
          <svg width={previewSize} height={previewSize} style={{ border: '1px solid #ddd', background: '#fff' }}>
            <path d={sectorPath(vals.rOuter, vals.rInner, endAngleRad, scale)} fill="#dbeafe" stroke="#0b5668" strokeWidth={1}/>
            {/* seam rectangle preview */}
            <polygon
              points={`
                ${seamPts.innerStart.x},${seamPts.innerStart.y}
                ${seamPts.outerStart.x},${seamPts.outerStart.y}
                ${seamPts.outerExtended.x},${seamPts.outerExtended.y}
                ${seamPts.innerExtended.x},${seamPts.innerExtended.y}
              `}
              fill="rgba(255,0,0,0.12)"
              stroke="red"
              strokeWidth={1}
            />
            {/* draw start radial line to show seam */}
            <line x1={seamPts.innerStart.x} y1={seamPts.innerStart.y} x2={seamPts.outerStart.x} y2={seamPts.outerStart.y} stroke="#222" strokeWidth={1}/>
          </svg>

          <div style={{ marginTop: 8 }}>
            <b>Hesaplar (mm):</b><br/>
            Dış yarıçap (pattern R) = {vals.rOuter.toFixed(3)} mm<br/>
            İç yarıçap = {vals.rInner.toFixed(3)} mm<br/>
            Sector açı = {vals.angleDeg.toFixed(3)}°<br/>
            Alt yay uzunluğu = {vals.outerArc.toFixed(3)} mm<br/>
            Üst yay uzunluğu = {vals.innerArc.toFixed(3)} mm
          </div>
        </div>
      </div>
    </div>
  );
}

// Render (CodePen: React + ReactDOM available globally)
const rootEl = document.getElementById('root');
if (rootEl) {
  // React 18 style
  if (ReactDOM.createRoot) {
    ReactDOM.createRoot(rootEl).render(<App />);
  } else {
    ReactDOM.render(<App />, rootEl);
  }
}