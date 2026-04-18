 import { useEffect, useRef } from "react";

function OrbCanvas({ hue = 0, hoverIntensity = 0.5, rotateOnHover = true }) {
  const containerRef = useRef(null);

  useEffect(() => {
    const container = containerRef.current;
    if (!container) return;

    const canvas = document.createElement("canvas");
    canvas.style.cssText = "position:absolute;top:0;left:0;width:100%;height:100%;";
    container.appendChild(canvas);

    const gl = canvas.getContext("webgl", { alpha: true, premultipliedAlpha: false });
    if (!gl) { container.removeChild(canvas); return; }
    gl.clearColor(0, 0, 0, 0);

    function compile(type, src) {
      const s = gl.createShader(type);
      gl.shaderSource(s, src);
      gl.compileShader(s);
      return s;
    }

    const vert = `precision highp float;
attribute vec2 position;
attribute vec2 uv;
varying vec2 vUv;
void main() { vUv = uv; gl_Position = vec4(position, 0.0, 1.0); }`;

    const frag = `precision highp float;
uniform float iTime; uniform vec3 iResolution; uniform float hue;
uniform float hover; uniform float rot; uniform float hoverIntensity;
uniform vec3 backgroundColor; varying vec2 vUv;
vec3 rgb2yiq(vec3 c){return vec3(dot(c,vec3(0.299,0.587,0.114)),dot(c,vec3(0.596,-0.274,-0.322)),dot(c,vec3(0.211,-0.523,0.312)));}
vec3 yiq2rgb(vec3 c){return vec3(c.x+0.956*c.y+0.621*c.z,c.x-0.272*c.y-0.647*c.z,c.x-1.106*c.y+1.703*c.z);}
vec3 adjustHue(vec3 color,float hueDeg){
  float hueRad=hueDeg*3.14159265/180.0; vec3 yiq=rgb2yiq(color);
  float cosA=cos(hueRad),sinA=sin(hueRad);
  float ni=yiq.y*cosA-yiq.z*sinA; float nq=yiq.y*sinA+yiq.z*cosA;
  return yiq2rgb(vec3(yiq.x,ni,nq));
}
vec3 hash33(vec3 p3){
  p3=fract(p3*vec3(0.1031,0.11369,0.13787)); p3+=dot(p3,p3.yxz+19.19);
  return -1.0+2.0*fract(vec3(p3.x+p3.y,p3.x+p3.z,p3.y+p3.z)*p3.zyx);
}
float snoise3(vec3 p){
  const float K1=0.333333333,K2=0.166666667;
  vec3 i=floor(p+(p.x+p.y+p.z)*K1);
  vec3 d0=p-(i-(i.x+i.y+i.z)*K2);
  vec3 e=step(vec3(0.0),d0-d0.yzx);
  vec3 i1=e*(1.0-e.zxy),i2=1.0-e.zxy*(1.0-e);
  vec3 d1=d0-(i1-K2),d2=d0-(i2-K1),d3=d0-0.5;
  vec4 h=max(0.6-vec4(dot(d0,d0),dot(d1,d1),dot(d2,d2),dot(d3,d3)),0.0);
  vec4 n=h*h*h*h*vec4(dot(d0,hash33(i)),dot(d1,hash33(i+i1)),dot(d2,hash33(i+i2)),dot(d3,hash33(i+1.0)));
  return dot(vec4(31.316),n);
}
vec4 extractAlpha(vec3 c){float a=max(max(c.r,c.g),c.b);return vec4(c/(a+1e-5),a);}
const vec3 baseColor1=vec3(0.611765,0.262745,0.996078),baseColor2=vec3(0.298039,0.760784,0.913725),baseColor3=vec3(0.062745,0.078431,0.600000);
const float innerRadius=0.6,noiseScale=0.65;
float light1(float i,float a,float d){return i/(1.0+d*a);}
float light2(float i,float a,float d){return i/(1.0+d*d*a);}
vec4 draw(vec2 uv){
  vec3 color1=adjustHue(baseColor1,hue),color2=adjustHue(baseColor2,hue),color3=adjustHue(baseColor3,hue);
  float ang=atan(uv.y,uv.x),len=length(uv),invLen=len>0.0?1.0/len:0.0;
  float bgL=dot(backgroundColor,vec3(0.299,0.587,0.114));
  float n0=snoise3(vec3(uv*noiseScale,iTime*0.5))*0.5+0.5;
  float r0=mix(mix(innerRadius,1.0,0.4),mix(innerRadius,1.0,0.6),n0);
  float d0=distance(uv,(r0*invLen)*uv);
  float v0=light1(1.0,10.0,d0)*smoothstep(r0*1.05,r0,len);
  v0*=mix(smoothstep(r0*0.8,r0*0.95,len),1.0,bgL*0.7);
  float cl=cos(ang+iTime*2.0)*0.5+0.5;
  vec2 pos=vec2(cos(-iTime),sin(-iTime))*r0;
  float d=distance(uv,pos);
  float v1=light2(1.5,5.0,d)*light1(1.0,50.0,d0);
  float v2=smoothstep(1.0,mix(innerRadius,1.0,n0*0.5),len);
  float v3=smoothstep(innerRadius,mix(innerRadius,1.0,0.5),len);
  vec3 colBase=mix(color1,color2,cl);
  float fadeAmount=mix(1.0,0.1,bgL);
  vec3 darkCol=clamp((mix(color3,colBase,v0)+v1)*v2*v3,0.0,1.0);
  vec3 lightCol=clamp(mix(backgroundColor,(colBase+v1)*mix(1.0,v2*v3,fadeAmount),v0),0.0,1.0);
  return extractAlpha(mix(darkCol,lightCol,bgL));
}
void main(){
  vec2 center=iResolution.xy*0.5; float sz=min(iResolution.x,iResolution.y);
  vec2 uv=(vUv*iResolution.xy-center)/sz*2.0;
  float s=sin(rot),c=cos(rot);
  uv=vec2(c*uv.x-s*uv.y,s*uv.x+c*uv.y);
  uv.x+=hover*hoverIntensity*0.1*sin(uv.y*10.0+iTime);
  uv.y+=hover*hoverIntensity*0.1*sin(uv.x*10.0+iTime);
  vec4 col=draw(uv);
  gl_FragColor=vec4(col.rgb*col.a,col.a);
}`;

    const vs = compile(gl.VERTEX_SHADER, vert);
    const fs = compile(gl.FRAGMENT_SHADER, frag);
    const prog = gl.createProgram();
    gl.attachShader(prog, vs); gl.attachShader(prog, fs); gl.linkProgram(prog); gl.useProgram(prog);

    const posArr = new Float32Array([-1,-1, 3,-1, -1,3]);
    const uvArr  = new Float32Array([0,0, 2,0, 0,2]);

    const posLoc = gl.getAttribLocation(prog, "position");
    const uvLoc  = gl.getAttribLocation(prog, "uv");

    const posBuf = gl.createBuffer();
    gl.bindBuffer(gl.ARRAY_BUFFER, posBuf);
    gl.bufferData(gl.ARRAY_BUFFER, posArr, gl.STATIC_DRAW);
    gl.enableVertexAttribArray(posLoc);
    gl.vertexAttribPointer(posLoc, 2, gl.FLOAT, false, 0, 0);

    const uvBuf = gl.createBuffer();
    gl.bindBuffer(gl.ARRAY_BUFFER, uvBuf);
    gl.bufferData(gl.ARRAY_BUFFER, uvArr, gl.STATIC_DRAW);
    gl.enableVertexAttribArray(uvLoc);
    gl.vertexAttribPointer(uvLoc, 2, gl.FLOAT, false, 0, 0);

    const uTime = gl.getUniformLocation(prog, "iTime");
    const uRes  = gl.getUniformLocation(prog, "iResolution");
    const uHue  = gl.getUniformLocation(prog, "hue");
    const uHov  = gl.getUniformLocation(prog, "hover");
    const uRot  = gl.getUniformLocation(prog, "rot");
    const uHI   = gl.getUniformLocation(prog, "hoverIntensity");
    const uBg   = gl.getUniformLocation(prog, "backgroundColor");

    gl.uniform1f(uHue, hue);
    gl.uniform1f(uHI, hoverIntensity);
    gl.uniform3f(uBg, 0, 0, 0);

    function resize() {
      const dpr = window.devicePixelRatio || 1;
      const w = container.clientWidth, h = container.clientHeight;
      canvas.width = w * dpr; canvas.height = h * dpr;
      canvas.style.width = w + "px"; canvas.style.height = h + "px";
      gl.viewport(0, 0, canvas.width, canvas.height);
      gl.uniform3f(uRes, canvas.width, canvas.height, canvas.width / canvas.height);
    }
    window.addEventListener("resize", resize);
    resize();

    let targetHover = 0, currentHover = 0, currentRot = 0, lastT = 0, rafId;
    function frame(t) {
      rafId = requestAnimationFrame(frame);
      const dt = Math.min((t - lastT) * 0.001, 0.05);
      lastT = t;
      gl.uniform1f(uTime, t * 0.001);
      currentHover += (targetHover - currentHover) * 0.1;
      gl.uniform1f(uHov, currentHover);
      if (rotateOnHover && currentHover > 0.1) currentRot += dt * 0.3;
      gl.uniform1f(uRot, currentRot);
      gl.enable(gl.BLEND);
      gl.blendFunc(gl.ONE, gl.ONE_MINUS_SRC_ALPHA);
      gl.clear(gl.COLOR_BUFFER_BIT);
      gl.bindBuffer(gl.ARRAY_BUFFER, posBuf);
      gl.vertexAttribPointer(posLoc, 2, gl.FLOAT, false, 0, 0);
      gl.bindBuffer(gl.ARRAY_BUFFER, uvBuf);
      gl.vertexAttribPointer(uvLoc, 2, gl.FLOAT, false, 0, 0);
      gl.drawArrays(gl.TRIANGLES, 0, 3);
    }
    requestAnimationFrame(frame);

    function onMove(e) {
      const r = container.getBoundingClientRect();
      const x = ((e.clientX - r.left) / r.width) * 2 - 1;
      const y = ((e.clientY - r.top) / r.height) * 2 - 1;
      targetHover = Math.sqrt(x * x + y * y) < 0.8 ? 1 : 0;
    }
    function onLeave() { targetHover = 0; }
    container.addEventListener("mousemove", onMove);
    container.addEventListener("mouseleave", onLeave);

    return () => {
      cancelAnimationFrame(rafId);
      window.removeEventListener("resize", resize);
      container.removeEventListener("mousemove", onMove);
      container.removeEventListener("mouseleave", onLeave);
      if (canvas.parentNode) canvas.parentNode.removeChild(canvas);
    };
  }, [hue, hoverIntensity, rotateOnHover]);

  return <div ref={containerRef} style={{ position: "absolute", inset: 0, zIndex: 0 }} />;
}

const skills = ["Veri Analizi", "R", "Python", "Analitik Beceriler", "Regression Testing"];

const education = [
  { school: "Dokuz Eylül University", dept: "Statistics", badge: "GPA: 3.45" },
  { school: "Istanbul University", dept: "Computer Programming" },
];

function SectionHeading({ children }) {
  return (
    <h2 style={{
      fontSize: "clamp(1.6rem,3.5vw,2.2rem)",
      fontWeight: 800,
      marginBottom: "2.5rem",
      letterSpacing: "-0.02em",
      display: "inline-block",
      position: "relative",
    }}>
      {children}
      <span style={{
        position: "absolute", bottom: -6, left: 0,
        width: "45%", height: "2px", borderRadius: 2,
        background: "linear-gradient(90deg,#9b4dff,#3cc4e8)",
      }} />
    </h2>
  );
}

export default function Portfolio() {
  return (
    <div style={{ background: "#000", color: "#fff", minHeight: "100vh", fontFamily: "'Syne', sans-serif" }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:wght@300;400;500&display=swap');
        *{margin:0;padding:0;box-sizing:border-box;}
        html{scroll-behavior:smooth;}
        a{text-decoration:none;color:inherit;}
        ::selection{background:rgba(155,77,255,0.35);}
      `}</style>

      {/* ── Navbar ── */}
      <nav style={{
        position: "fixed", top: 0, left: 0, right: 0, zIndex: 100,
        display: "flex", alignItems: "center", justifyContent: "space-between",
        padding: "1.25rem 3rem",
        background: "rgba(0,0,0,0.25)",
        backdropFilter: "blur(12px)",
        borderBottom: "1px solid rgba(255,255,255,0.06)",
      }}>
        <span style={{ fontWeight: 800, fontSize: "1.25rem", letterSpacing: "0.06em" }}>MMÖ</span>
        <div style={{ display: "flex", gap: "2.5rem" }}>
          {["About", "Experience", "Education"].map(l => (
            <a
              key={l}
              href={`#${l.toLowerCase()}`}
              style={{ opacity: 0.7, fontSize: "0.9rem", fontWeight: 500, letterSpacing: "0.05em", transition: "opacity .2s" }}
              onMouseEnter={e => (e.target.style.opacity = 1)}
              onMouseLeave={e => (e.target.style.opacity = 0.7)}
            >{l}</a>
          ))}
        </div>
      </nav>

      {/* ── Hero ── */}
      <section style={{
        height: "100vh", display: "flex", alignItems: "center",
        justifyContent: "center", background: "#000", overflow: "hidden",
      }}>
        {/* Orb wrapper — square, relative so both orb and text overlay reference it */}
        <div style={{
          position: "relative",
          width: "min(680px, 88vmin)",
          height: "min(680px, 88vmin)",
        }}>
          {/* WebGL Orb fills the wrapper absolutely */}
          <OrbCanvas hue={0} hoverIntensity={0.5} rotateOnHover={true} />

          {/* Text overlay — pointer-events:none so orb hover still fires */}
          <div style={{
            position: "absolute", inset: 0, zIndex: 10,
            display: "flex", flexDirection: "column",
            alignItems: "center", justifyContent: "center",
            pointerEvents: "none",
            padding: "2.5rem",
          }}>
            <h1 style={{
              fontSize: "clamp(1.5rem, 4.5vw, 2.6rem)",
              fontWeight: 800,
              color: "#fff",
              textAlign: "center",
              lineHeight: 1.15,
              marginBottom: "0.7rem",
              letterSpacing: "-0.01em",
              fontFamily: "'Syne', sans-serif",
              textShadow: "0 2px 24px rgba(0,0,0,0.7)",
            }}>
              Melisa Meltem Özmen
            </h1>
            <p style={{
              fontSize: "clamp(0.78rem, 1.6vw, 0.98rem)",
              opacity: 0.8,
              textAlign: "center",
              marginBottom: "2rem",
              fontFamily: "'DM Sans', sans-serif",
              fontWeight: 400,
              textShadow: "0 1px 12px rgba(0,0,0,0.8)",
            }}>
              Statistics Student&nbsp;|&nbsp;Prospective Data Scientist
            </p>

            {/* Buttons re-enable pointer events */}
            <div style={{ display: "flex", gap: "0.75rem", pointerEvents: "auto" }}>
              <button
                onClick={() => window.open("https://mail.google.com/mail/?view=cm&fs=1&to=melisameltemozmen@gmail.com", "_blank")}
                style={{
                  padding: "0.6rem 1.6rem",
                  background: "#fff", color: "#000",
                  border: "none", borderRadius: "100px",
                  fontWeight: 700, fontSize: "0.88rem",
                  cursor: "pointer", fontFamily: "'Syne', sans-serif",
                  letterSpacing: "0.02em", transition: "transform .15s,opacity .15s",
                }}
                onMouseEnter={e => (e.currentTarget.style.opacity = "0.9")}
                onMouseLeave={e => (e.currentTarget.style.opacity = "1")}
              >
                Message
              </button>
              <button
                style={{
                  padding: "0.6rem 1.6rem",
                  background: "rgba(255,255,255,0.07)", color: "#fff",
                  border: "1px solid rgba(255,255,255,0.28)", borderRadius: "100px",
                  fontWeight: 700, fontSize: "0.88rem",
                  cursor: "pointer", backdropFilter: "blur(8px)",
                  fontFamily: "'Syne', sans-serif", letterSpacing: "0.02em",
                  transition: "background .15s",
                }}
                onMouseEnter={e => (e.currentTarget.style.background = "rgba(255,255,255,0.14)")}
                onMouseLeave={e => (e.currentTarget.style.background = "rgba(255,255,255,0.07)")}
              >
                Resume
              </button>
            </div>

            {/* Social Icons */}
            <div style={{ display: "flex", gap: "1rem", marginTop: "1.5rem", pointerEvents: "auto" }}>
              <a
                href="https://mail.google.com/mail/?view=cm&fs=1&to=melisameltemozmen@gmail.com"
                target="_blank" rel="noreferrer" title="melisameltemozmen@gmail.com"
                style={{ width:40, height:40, borderRadius:"50%", display:"flex", alignItems:"center", justifyContent:"center", background:"rgba(255,255,255,0.08)", border:"1px solid rgba(255,255,255,0.2)", backdropFilter:"blur(8px)", transition:"background .2s,border-color .2s", cursor:"pointer" }}
                onMouseEnter={e => { e.currentTarget.style.background="rgba(255,255,255,0.18)"; e.currentTarget.style.borderColor="rgba(255,255,255,0.45)"; }}
                onMouseLeave={e => { e.currentTarget.style.background="rgba(255,255,255,0.08)"; e.currentTarget.style.borderColor="rgba(255,255,255,0.2)"; }}
              >
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M22 6C22 4.9 21.1 4 20 4H4C2.9 4 2 4.9 2 6V18C2 19.1 2.9 20 4 20H20C21.1 20 22 19.1 22 18V6ZM20 6L12 11L4 6H20ZM20 18H4V8L12 13L20 8V18Z" fill="white" fillOpacity="0.85"/>
                </svg>
              </a>
              <a
                href="https://www.linkedin.com/in/melisameltemozmen"
                target="_blank" rel="noreferrer" title="LinkedIn"
                style={{ width:40, height:40, borderRadius:"50%", display:"flex", alignItems:"center", justifyContent:"center", background:"rgba(255,255,255,0.08)", border:"1px solid rgba(255,255,255,0.2)", backdropFilter:"blur(8px)", transition:"background .2s,border-color .2s", cursor:"pointer" }}
                onMouseEnter={e => { e.currentTarget.style.background="rgba(255,255,255,0.18)"; e.currentTarget.style.borderColor="rgba(255,255,255,0.45)"; }}
                onMouseLeave={e => { e.currentTarget.style.background="rgba(255,255,255,0.08)"; e.currentTarget.style.borderColor="rgba(255,255,255,0.2)"; }}
              >
                <svg width="17" height="17" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                  <path fill="rgba(255,255,255,0.85)" d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                </svg>
              </a>
            </div>
          </div>
        </div>
      </section>

      {/* ── About ── */}
      <section id="about" style={{ padding: "7rem 2rem", maxWidth: 860, margin: "0 auto" }}>
        <SectionHeading>About</SectionHeading>
        <p style={{
          fontSize: "1.05rem", lineHeight: 1.9, opacity: 0.8,
          marginBottom: "2.5rem", fontFamily: "'DM Sans', sans-serif",
          maxWidth: 700,
        }}>
          I am currently studying Statistics at Dokuz Eylül University and Computer
          Programming at Istanbul University. My goal is to combine statistical methods
          with programming to create data-driven solutions. I have experience using R and
          Python for data analysis, specifically focusing on regression models and
          hypothesis testing.
        </p>
        <div style={{ display: "flex", flexWrap: "wrap", gap: "0.55rem" }}>
          {skills.map(s => (
            <span key={s} style={{
              padding: "0.4rem 1rem",
              border: "1px solid rgba(155,77,255,0.4)",
              borderRadius: "100px",
              fontSize: "0.82rem",
              fontFamily: "'DM Sans', sans-serif",
              background: "rgba(155,77,255,0.08)",
              color: "#c9aaff",
              letterSpacing: "0.02em",
            }}>{s}</span>
          ))}
        </div>
      </section>

      <div style={{ maxWidth: 860, margin: "0 auto", height: 1, background: "rgba(255,255,255,0.07)" }} />

      {/* ── Experience ── */}
      <section id="experience" style={{ padding: "7rem 2rem", maxWidth: 860, margin: "0 auto" }}>
        <SectionHeading>Experience</SectionHeading>
        <div style={{
          position: "relative",
          borderLeft: "2px solid rgba(155,77,255,0.3)",
          paddingLeft: "2rem",
        }}>
          {/* Timeline dot */}
          <div style={{
            position: "absolute", left: -6, top: 5,
            width: 11, height: 11, borderRadius: "50%",
            background: "linear-gradient(135deg,#9b4dff,#3cc4e8)",
          }} />
          <h3 style={{ fontSize: "1.1rem", fontWeight: 700, marginBottom: "0.25rem" }}>
            Stajyer Öğrenci
          </h3>
          <p style={{ opacity: 0.65, fontFamily: "'DM Sans', sans-serif", marginBottom: "0.5rem", fontSize: "0.95rem" }}>
            DenizBank
          </p>
          <span style={{
            fontSize: "0.78rem", padding: "0.2rem 0.8rem",
            background: "rgba(60,196,232,0.1)",
            border: "1px solid rgba(60,196,232,0.3)",
            borderRadius: "100px", color: "#3cc4e8",
            fontFamily: "'DM Sans', sans-serif",
          }}>2024</span>
        </div>
      </section>

      <div style={{ maxWidth: 860, margin: "0 auto", height: 1, background: "rgba(255,255,255,0.07)" }} />

      {/* ── Education ── */}
      <section id="education" style={{ padding: "7rem 2rem", maxWidth: 860, margin: "0 auto" }}>
        <SectionHeading>Education</SectionHeading>
        <div style={{
          position: "relative",
          borderLeft: "2px solid rgba(155,77,255,0.3)",
          paddingLeft: "2rem",
          display: "flex", flexDirection: "column", gap: "2.5rem",
        }}>
          {education.map((edu, i) => (
            <div key={i} style={{ position: "relative" }}>
              <div style={{
                position: "absolute", left: "calc(-2rem - 5px)", top: 5,
                width: 11, height: 11, borderRadius: "50%",
                background: "linear-gradient(135deg,#9b4dff,#3cc4e8)",
              }} />
              <h3 style={{ fontSize: "1.1rem", fontWeight: 700, marginBottom: "0.25rem" }}>
                {edu.school}
              </h3>
              <p style={{ opacity: 0.65, fontFamily: "'DM Sans', sans-serif", marginBottom: edu.badge ? "0.5rem" : 0, fontSize: "0.95rem" }}>
                {edu.dept}
              </p>
              {edu.badge && (
                <span style={{
                  fontSize: "0.78rem", padding: "0.2rem 0.8rem",
                  background: "rgba(155,77,255,0.1)",
                  border: "1px solid rgba(155,77,255,0.3)",
                  borderRadius: "100px", color: "#c9aaff",
                  fontFamily: "'DM Sans', sans-serif",
                }}>{edu.badge}</span>
              )}
            </div>
          ))}
        </div>
      </section>

      {/* ── Footer ── */}
      <footer style={{ borderTop: "1px solid rgba(255,255,255,0.07)", padding: "3rem 2rem 2.5rem", fontFamily: "'DM Sans', sans-serif" }}>
        <div style={{ maxWidth: 860, margin: "0 auto", display: "flex", flexDirection: "column", alignItems: "center", gap: "1.25rem" }}>
          <div style={{ display: "flex", alignItems: "center", gap: "1.5rem", flexWrap: "wrap", justifyContent: "center" }}>
            <a
              href="https://mail.google.com/mail/?view=cm&fs=1&to=melisameltemozmen@gmail.com"
              target="_blank" rel="noreferrer"
              style={{ display:"flex", alignItems:"center", gap:"0.45rem", opacity:0.55, fontSize:"0.84rem", transition:"opacity .2s", color:"#fff", textDecoration:"none" }}
              onMouseEnter={e => (e.currentTarget.style.opacity="1")}
              onMouseLeave={e => (e.currentTarget.style.opacity="0.55")}
            >
              <svg width="15" height="15" viewBox="0 0 24 24" fill="none"><path d="M22 6C22 4.9 21.1 4 20 4H4C2.9 4 2 4.9 2 6V18C2 19.1 2.9 20 4 20H20C21.1 20 22 19.1 22 18V6ZM20 6L12 11L4 6H20ZM20 18H4V8L12 13L20 8V18Z" fill="white"/></svg>
              melisameltemozmen@gmail.com
            </a>
            <span style={{ opacity:0.2 }}>·</span>
            <a
              href="https://www.linkedin.com/in/melisameltemozmen"
              target="_blank" rel="noreferrer"
              style={{ display:"flex", alignItems:"center", gap:"0.45rem", opacity:0.55, fontSize:"0.84rem", transition:"opacity .2s", color:"#fff", textDecoration:"none" }}
              onMouseEnter={e => (e.currentTarget.style.opacity="1")}
              onMouseLeave={e => (e.currentTarget.style.opacity="0.55")}
            >
              <svg width="14" height="14" viewBox="0 0 24 24"><path fill="white" d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
              linkedin.com/in/melisameltemozmen
            </a>
            <span style={{ opacity:0.2 }}>·</span>
            <span style={{ display:"flex", alignItems:"center", gap:"0.4rem", opacity:0.45, fontSize:"0.84rem", color:"#fff" }}>
              <svg width="13" height="13" viewBox="0 0 24 24" fill="none"><path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z" fill="white"/></svg>
              İstanbul / İzmir, Türkiye
            </span>
          </div>
          <p style={{ opacity:0.22, fontSize:"0.78rem", color:"#fff" }}>© 2024 Melisa Meltem Özmen — All rights reserved</p>
        </div>
      </footer>
    </div>
  );
}
