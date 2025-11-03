# trabzon-info
#!/usr/bin/env python3
else:
return None, f"API hatası: {resp.status_code}"
except requests.exceptions.RequestException as e:
return None, str(e)




def format_weather(data):
main = data.get("main", {})
weather = data.get("weather", [{}])[0]
wind = data.get("wind", {})
lines = []
lines.append(f"Trabzon — {datetime.now().strftime('%Y-%m-%d %H:%M')}")
lines.append(f"Sıcaklık: {main.get('temp')} °C (Hissedilen: {main.get('feels_like')} °C)")
lines.append(f"Nem: {main.get('humidity')}%")
lines.append(f"Rüzgar: {wind.get('speed')} m/s")
lines.append(f"Durum: {weather.get('description', '').capitalize()}")
return "\n".join(lines)




def print_touristic_spots():
lines = ["\nTrabzon - Öne çıkan yerler:"]
for i, s in enumerate(TOURISTIC_SPOTS, 1):
lines.append(f"{i}. {s['name']} — {s['desc']}")
return "\n".join(lines)




def save_output(text, path="trabzon_info.txt"):
with open(path, "w", encoding="utf-8") as f:
f.write(text)




def main(save=False):
data, err = get_trabzon_weather()
parts = []
if err:
parts.append(f"Hava durumu alınamadı: {err}")
else:
parts.append(format_weather(data))


parts.append(print_touristic_spots())
out = "\n\n".join(parts)
print(out)


if save:
save_output(out)
print(f"\nÇıktı kaydedildi: trabzon_info.txt")




if __name__ == "__main__":
save_flag = "--save" in sys.argv or "-s" in sys.argv
main(save=save_flag)
# 1. Repo dizini oluştur
mkdir trabzon-info
cd trabzon-info


# 2. Dosyaları oluştur (kodu kopyala yapıştır)
# - trabzon.py
# - requirements.txt
# - README.md


# 3. Git başlat
git init
git add .
git commit -m "İlk commit: Trabzon info CLI"


# 4. GitHub'da oluşturduğun repo URL'sini bağla (örnek):
git remote add origin https://github.com/<kullanici_adiniz>/trabzon-info.git


# 5. Push et
git branch -M main
git push -u origin main
