from moviepy.editor import *

# مسار الصورة (غير الاسم حسب الحاجة)
image_path = "property_image.png"

# تحميل الصورة وتحديد مدة الفيديو
image_clip = ImageClip(image_path).set_duration(10)

# تكبير بسيط للصورة لتطبيق حركة تدريجية (zoom/pan)
image_clip = image_clip.resize(height=2200)

# تطبيق حركة بان لأعلى وتكبير تدريجي خفيف
animated_clip = image_clip.set_position(lambda t: ("center", int(50 - 10*t))) \
                          .resize(lambda t: 1 + 0.01 * t)

# ضبط أبعاد الفيديو لتكون 9:16 (مثل شاشة الجوال)
final_clip = animated_clip.set_fps(24).resize((1080, 1920))

# تصدير الفيديو
final_clip.write_videofile("property_for_sale_video.mp4", codec="libx264", audio=False)
