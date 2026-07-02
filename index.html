import gradio as gr
from PIL import Image, ImageEnhance, ImageDraw
import tempfile
import os
import math

# ==========================================
# 🎨 [컬러 설정] 이곳에서 원하는 컬러코드로 변경하세요!
# ==========================================
EFFECT_R, EFFECT_G, EFFECT_B = 0, 255, 255  # RGB 값 (예: 시안색 0, 255, 255)
EFFECT_HEX = "#00ffff"                      # HEX 코드
# ==========================================

custom_css = f"""
body, gradio-app {{ 
    background-color: #0a0f18 !important; 
}}
.gradio-container {{
    background-color: #111a28 !important;
    border: 1px solid {EFFECT_HEX} !important;
    box-shadow: 0 0 15px rgba({EFFECT_R}, {EFFECT_G}, {EFFECT_B}, 0.2) !important;
    border-radius: 8px !important;
    max-width: 500px !important;
    margin: 40px auto !important;
    padding: 30px !important;
}}
.title-text {{
    color: {EFFECT_HEX} !important;
    font-size: 26px !important;
    text-align: center !important;
    font-weight: bold !important;
    margin-bottom: 5px !important;
    text-shadow: 0 0 10px rgba({EFFECT_R}, {EFFECT_G}, {EFFECT_B}, 0.5) !important;
    font-family: 'Malgun Gothic', 'Apple SD Gothic Neo', sans-serif !important;
    letter-spacing: 1px;
}}
.subtitle-text {{
    color: #8888aa !important;
    text-align: center !important;
    font-size: 13px !important;
    margin-bottom: 25px !important;
    font-family: 'Malgun Gothic', 'Apple SD Gothic Neo', sans-serif !important;
}}
#action-btn {{
    background-color: transparent !important;
    border: 2px solid {EFFECT_HEX} !important;
    color: {EFFECT_HEX} !important;
    padding: 10px !important;
    font-size: 16px !important;
    font-weight: bold !important;
    border-radius: 4px !important;
    cursor: pointer !important;
    margin-top: 15px !important;
    transition: 0.3s;
}}
#action-btn:hover {{
    background-color: {EFFECT_HEX} !important;
    color: #111a28 !important;
    box-shadow: 0 0 15px rgba({EFFECT_R}, {EFFECT_G}, {EFFECT_B}, 0.5) !important;
}}
footer {{ display: none !important; }}
"""

custom_head = """
<meta property="og:title" content="[ SYSTEM : SF POPUP GENERATOR ]">
<meta property="og:description" content="코코포리아 마커 패널용 SF 컷인 생성기">
<meta property="og:image" content="https://huggingface.co/spaces/Nyacha/SF-Popup-Generator/resolve/main/preview.png?download=true">
<meta name="twitter:card" content="summary_large_image">
"""

def generate_sf_popup(input_path):
    if input_path is None:
        return None
        
    original_filename = os.path.basename(input_path)
    name_only, _ = os.path.splitext(original_filename)
    output_filename = f"SF_{name_only}.webp" 
        
    img = Image.open(input_path).convert("RGBA")
    w, h = img.size
    max_width = 800 

    if w > max_width:
        scale = max_width / w
        new_w, new_h = int(w * scale), int(h * scale)
        img = img.resize((new_w, new_h), Image.Resampling.LANCZOS)
        w, h = new_w, new_h

    frame_list, durations = [], []

    # 1. 대기 프레임
    frame_list.append(Image.new("RGBA", (w, h), (0, 0, 0, 0)))
    durations.append(100)

    # 2. 점에서 시작하여 터지는 렌즈 플레어 효과 (더 세밀한 4단계 설정)
    sparkle_phases = [
        (0.01, 100, 40),  # 1단계: 가운데 미세한 점 등장
        (0.06, 220, 30),  # 2단계: 빛이 응축되며 살짝 커짐
        (0.45, 255, 50),  # 3단계: 팟! 하고 크게 터짐
        (0.12, 160, 40)   # 4단계: 잔상과 함께 수축
    ]
    
    for size_ratio, alpha, duration in sparkle_phases:
        s_frame = Image.new("RGBA", (w, h), (0, 0, 0, 0))
        draw = ImageDraw.Draw(s_frame)
        cx, cy = w // 2, h // 2
        
        r = max(2, int(min(w, h) * size_ratio)) 
        inner_r = max(1, int(r * 0.15))

        flare_w, flare_h = int(w * size_ratio * 1.5), max(2, int(h * 0.015))
        draw.rectangle([cx - flare_w, cy - flare_h, cx + flare_w, cy + flare_h], fill=(EFFECT_R, EFFECT_G, EFFECT_B, int(alpha * 0.7)))

        points = [(cx, cy - r), (cx + inner_r, cy - inner_r), (cx + r, cy), (cx + inner_r, cy + inner_r), 
                  (cx, cy + r), (cx - inner_r, cy + inner_r), (cx - r, cy), (cx - inner_r, cy - inner_r)]
        draw.polygon(points, fill=(EFFECT_R, EFFECT_G, EFFECT_B, alpha))
        
        cr = max(1, int(inner_r * 1.2))
        draw.ellipse([cx - cr, cy - cr, cx + cr, cy + cr], fill=(255, 255, 255, alpha))
        
        frame_list.append(s_frame)
        durations.append(duration) 

    # 3. 레이저 잔상
    fh1 = max(2, int(h * 0.015)) 
    ty1 = (h - fh1) // 2
    flash_line1 = img.crop((0, ty1, w, ty1 + fh1))
    color_solid1 = Image.new("RGBA", flash_line1.size, (EFFECT_R, EFFECT_G, EFFECT_B, 200))
    color_solid1.putalpha(flash_line1.split()[3]) 
    c_flash1 = Image.new("RGBA", (w, h), (0, 0, 0, 0))
    c_flash1.paste(color_solid1, (0, ty1))
    frame_list.append(c_flash1)
    durations.append(30) 

    # 4. 레이저 굵어짐
    fh2 = max(4, int(h * 0.08)) 
    ty2 = (h - fh2) // 2
    flash_line2 = img.crop((0, ty2, w, ty2 + fh2))
    color_solid2 = Image.new("RGBA", flash_line2.size, (EFFECT_R, EFFECT_G, EFFECT_B, 255))
    color_solid2.putalpha(flash_line2.split()[3])
    mixed_flash = Image.blend(flash_line2, color_solid2, alpha=0.8)
    mixed_flash = ImageEnhance.Brightness(mixed_flash).enhance(2.5)
    c_flash2 = Image.new("RGBA", (w, h), (0, 0, 0, 0))
    c_flash2.paste(mixed_flash, (0, ty2))
    frame_list.append(c_flash2)
    durations.append(40)

    # 5. 홀로그램 전개 
    frames = 15 
    for i in range(1, frames + 1):
        t = i / frames
        ease_t = 1 - pow(1 - t, 3) 
        ch = max(1, min(h, int(h * ease_t)))
        ty = (h - ch) // 2
        cropped = img.crop((0, ty, w, ty + ch))
        
        tint_ratio = (1 - ease_t) * 0.7
        if tint_ratio > 0.01:
            color_overlay = Image.new("RGBA", cropped.size, (EFFECT_R, EFFECT_G, EFFECT_B, 255))
            color_overlay.putalpha(cropped.split()[3]) 
            cropped = Image.blend(cropped, color_overlay, alpha=tint_ratio)
        
        c = Image.new("RGBA", (w, h), (0, 0, 0, 0))
        c.paste(cropped, (0, ty))
        frame_list.append(c)
        durations.append(450 // frames)

    temp_dir = tempfile.gettempdir()
    out_path = os.path.join(temp_dir, output_filename)
    
    frame_list[0].save(out_path, save_all=True, append_images=frame_list[1:], 
                       format="WebP", duration=durations, loop=1, lossless=False, quality=90)
    
    return out_path

with gr.Blocks(css=custom_css, theme=gr.themes.Base(), head=custom_head, title="SF POPUP GENERATOR") as app:
    gr.HTML("<div class='title-text'>[ SYSTEM : SF POPUP ]</div>")
    gr.HTML("<div class='subtitle-text'>이미지를 첨부하면 마커 패널용 SF 컷인이 생성됩니다.</div>")
    
    with gr.Column():
        image_input = gr.Image(type="filepath", label="이미지 업로드", show_label=False)
        submit_btn = gr.Button("SF 애니메이션 생성 시작", elem_id="action-btn")
        file_output = gr.File(label="완성된 파일 다운로드", show_label=False)
            
    submit_btn.click(fn=generate_sf_popup, inputs=image_input, outputs=file_output)

if __name__ == "__main__":
    app.launch()
