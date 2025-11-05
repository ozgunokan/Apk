git clone https://github.com/openwrt/openwrt.git openwrt-cerrahi
cd openwrt-cerrahi

git checkout v24.10.2
git switch -c onhub-stabil-cerrahi
git remote add asvio https://github.com/asvio/R7800-nss.git
git fetch asvio
git log v24.10.2..asvio/r7800-24.10-nss --oneline

# === OTOMATİK AMELİYAT LİSTESİ BAŞLANGICI ===

# --- Temel IPQ806X ve Ağ Yapısı Ayarları ---
git cherry-pick 02bd399f7a && \
git cherry-pick 995ead6af4 && \

# --- NSS ve Wi-Fi Desteğinin Temelleri ---
git cherry-pick 64f8c6041c && \
git cherry-pick ae515661e3 && \
git cherry-pick 40a4393e43 && \
git cherry-pick cc6b324ee7 && \
git cherry-pick 3e772c843c && \

# --- Wi-Fi QAM-256 (Yüksek Hız) Desteği ---
git cherry-pick 290156f351 && \
git cherry-pick 0073a62855 && \
git cherry-pick 414d298cc0 && \
git cherry-pick 85c4e61904 && \
git cherry-pick 7e98164278 && \

# --- Çeşitli Düzeltmeler ve İyileştirmeler ---
git cherry-pick 07f72b8283 && \
git cherry-pick 6cd56ad439 && \
git cherry-pick 8921799a20 && \
git cherry-pick 2fc66047fc && \
git cherry-pick 8f21c0bbb9 && \
git cherry-pick c81a0743e6 && \
git cherry-pick 22985bce50 && \
git cherry-pick abc096ab76 && \
git cherry-pick 056b68da27 && \
git cherry-pick 95fa6e7288 && \
git cherry-pick 7233c8f9ee && \
git cherry-pick 265e79f908 && \
git cherry-pick 47d9212ec5 && \
git cherry-pick 6222161586 && \
git cherry-pick 0fdd225dc7 && \
git cherry-pick 5a4fc73b57 && \
git cherry-pick e9bc6318c0 && \
git cherry-pick b1463dc066 && \
git cherry-pick a4f92df8fe && \
git cherry-pick 31577da363 && \
git cherry-pick 2d8ae61b6e && \
git cherry-pick b6d0270d7c && \

# --- En Güncel Kernel ve Mac80211 Yamaları ---
git cherry-pick 998892d067 && \
git cherry-pick e7b322f14d && \
git cherry-pick 58a9b0ac2e && \

echo ">>> Otomatik yama uygulama işlemi tamamlandı veya bir çatışma nedeniyle durdu."

# === OTOMATİK AMELİYAT LİSTESİ BİTİŞİ ===


git checkout --theirs feeds.conf.default
git add .
git cherry-pick --continue

# === KALAN YAMALAR ===

git cherry-pick 22985bce50 && \
git cherry-pick abc096ab76 && \
git cherry-pick 056b68da27 && \
git cherry-pick 95fa6e7288 && \
git cherry-pick 7233c8f9ee && \
git cherry-pick 265e79f908 && \
git cherry-pick 47d9212ec5 && \
git cherry-pick 6222161586 && \
git cherry-pick 0fdd225dc7 && \
git cherry-pick 5a4fc73b57 && \
git cherry-pick e9bc6318c0 && \
git cherry-pick b1463dc066 && \
git cherry-pick a4f92df8fe && \
git cherry-pick 31577da363 && \
git cherry-pick 2d8ae61b6e && \
git cherry-pick b6d0270d7c && \
git cherry-pick 998892d067 && \
git cherry-pick e7b322f14d && \
git cherry-pick 58a9b0ac2e && \

echo ">>> Tüm yamalar başarıyla uygulandı!"

./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make -j$(nproc)
