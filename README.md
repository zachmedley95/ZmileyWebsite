# ZmileyWebsite
Website for my music 
import { useState, useEffect } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { motion, AnimatePresence, useScroll, useTransform } from "framer-motion";
import { Music, ShoppingBag, Mail, Instagram, Youtube, Play, Facebook, X } from "lucide-react";

export default function ZmileyOfficial() {
  const { scrollY } = useScroll();
  const logoRotate = useTransform(scrollY, [0, 2000], [0, 40]);
  const logoY = useTransform(scrollY, [0, 2000], [0, -200]);

  const [email, setEmail] = useState("");
  const [secretClicks, setSecretClicks] = useState(0);
  const [quickView, setQuickView] = useState(null);
  const [intro, setIntro] = useState(true);

  useEffect(() => {
    const timer = setTimeout(() => setIntro(false), 2600);
    return () => clearTimeout(timer);
  }, []);

  const easterEgg = () => {
    const newCount = secretClicks + 1;
    setSecretClicks(newCount);

    if (newCount === 7) {
      alert("Thank you for being a loyal fan");
      setSecretClicks(0);
    }
  };

  const merchItems = [
    { name: "Zmiley Hoodie", image: "/mnt/data/Zmiley hoodie.jpg" },
    { name: "Zmiley T-Shirt", image: "/mnt/data/Zmiley tshirt.jpg" },
    { name: "Zmiley Poster", image: "/mnt/data/zmiley poster.jpg" }
  ];

  return (
    <>
      <style>{`
        @keyframes zmileyFlicker {
          0%,18%,22%,25%,53%,57%,100% { opacity:1; text-shadow:0 0 10px #ff0000,0 0 20px #ff0000,0 0 40px #ff0000; }
          20%,24%,55% { opacity:0.6; text-shadow:0 0 4px #ff0000,0 0 10px #ff0000; }
        }
        .zmiley-neon { color:black; animation: zmileyFlicker 2.5s infinite; }
      `}</style>

      <div className="min-h-screen bg-black text-white overflow-x-hidden">

        {/* INTRO LOGO FORMATION */}
        <AnimatePresence>
          {intro && (
            <motion.div
              className="fixed inset-0 z-[200] bg-black flex items-center justify-center overflow-hidden"
              initial={{ opacity: 1 }}
              exit={{ opacity: 0 }}
              transition={{ duration: 1 }}
            >

              {[...Array(120)].map((_, i) => (
                <motion.div
                  key={i}
                  className="absolute w-[2px] h-[2px] bg-white rounded-full"
                  initial={{
                    x: Math.random() * 1000 - 500,
                    y: Math.random() * 1000 - 500,
                    opacity: 0
                  }}
                  animate={{
                    x: 0,
                    y: 0,
                    opacity: [0, 1, 0.6]
                  }}
                  transition={{ duration: 2, delay: i * 0.01 }}
                />
              ))}

              <motion.h1
                className="text-5xl md:text-8xl font-bold tracking-[0.35em] zmiley-neon"
                initial={{ opacity: 0, scale: 0.7 }}
                animate={{ opacity: 1, scale: 1 }}
                transition={{ delay: 1.2, duration: 0.8 }}
              >
                ZMILEY
              </motion.h1>
            </motion.div>
          )}
        </AnimatePresence>

        {/* BACKGROUND */}
        <div className="fixed inset-0 -z-10 overflow-hidden">

          <motion.img
            src="/mnt/data/Zmiley_20251022_182913_0000.png"
            alt="Zmiley background"
            style={{ rotate: logoRotate, y: logoY }}
            className="absolute inset-0 w-full h-full object-contain opacity-10 pointer-events-none select-none"
          />

          {[...Array(80)].map((_, i) => (
            <motion.div
              key={i}
              className="absolute w-[2px] h-[2px] bg-white rounded-full"
              animate={{
                y: ["0%", "100%"],
                opacity: [0.1, 1, 0.1],
                scale: [1, 1.8, 1]
              }}
              transition={{ duration: 15 + i, repeat: Infinity }}
              style={{ left: `${Math.random() * 100}%`, top: `${Math.random() * 100}%` }}
            />
          ))}

        </div>

        {/* NAVBAR */}
        <nav className="fixed top-0 w-full z-50 backdrop-blur bg-black/40 border-b border-neutral-900">
          <div className="flex items-center justify-between px-4 md:px-8 py-4 md:py-5 max-w-7xl mx-auto">

            <h1 onClick={easterEgg} className="text-lg md:text-xl font-bold tracking-[0.3em] cursor-pointer zmiley-neon">
              ZMILEY
            </h1>

            <div className="hidden md:flex gap-8 text-sm text-gray-300">
              <a href="#music" className="hover:text-white">Music</a>
              <a href="#merch" className="hover:text-white">Merch</a>
              <a href="#community" className="hover:text-white">Community</a>
            </div>

          </div>
        </nav>

        {/* HERO */}
        <section className="relative h-screen flex items-center justify-center text-center px-6">

          <video autoPlay muted loop playsInline className="absolute w-full h-full object-cover opacity-40">
            <source src="/hero-video.mp4" type="video/mp4" />
          </video>

          <div className="absolute inset-0 bg-gradient-to-b from-black/70 via-black/50 to-black" />

          <motion.div
            initial={{ opacity: 0, y: 40 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 1 }}
            className="relative z-10"
          >

            <h1 className="text-5xl md:text-9xl font-bold tracking-tight zmiley-neon">ZMILEY</h1>

            <p className="mt-6 text-gray-300 text-lg md:text-xl">Music • Visuals • Universe</p>

            <div className="mt-10 flex flex-col md:flex-row justify-center gap-4">
              <Button className="flex gap-2 items-center text-lg px-8 py-6">
                <Music size={18}/> Listen
              </Button>

              <Button
                className="flex gap-2 items-center text-lg px-8 py-6"
                onClick={() => window.open("https://zmileymerch.printify.me/", "_blank")}
              >
                <ShoppingBag size={18}/> Merch
              </Button>
            </div>
          </motion.div>

        </section>

        {/* MUSIC */}
        <section id="music" className="px-6 py-32">
          <div className="max-w-7xl mx-auto">

            <h2 className="text-5xl font-bold mb-16">Music</h2>

            <div className="grid md:grid-cols-3 gap-10">

              {[
                { name: "I'm Here", link: "https://open.spotify.com/track/512HmPFjyI7IzCZHI4wBvF?si=3054cea47eb84d3c" },
                { name: "Wait", link: "https://open.spotify.com/track/7yFpA9L62ztBZSajHgJUIe?si=02a73af4ab0c4990" },
                { name: "My Baby", link: "https://open.spotify.com/track/0UezIlETXp2SoTbxR287w0?si=32da11918b34490f" }
              ].map((song) => (
                <Card key={song.name} className="bg-neutral-900 border-neutral-800 hover:scale-105 transition">
                  <CardContent className="p-8">
                    <h3 className="text-2xl font-semibold text-white">{song.name}</h3>
                    <p className="text-gray-400 mt-2">Streaming everywhere</p>
                    <Button className="mt-6 w-full flex gap-2 items-center justify-center" onClick={() => window.open(song.link, "_blank")}>
                      <Play size={16}/> Play
                    </Button>
                  </CardContent>
                </Card>
              ))}

            </div>

          </div>
        </section>

        {/* MERCH */}
        <section id="merch" className="px-6 py-32 bg-neutral-950">

          <div className="max-w-7xl mx-auto text-center">

            <h2 className="text-5xl font-bold mb-10">Official Merch</h2>

            <div className="grid md:grid-cols-3 gap-10 mb-16">

              {merchItems.map((item) => (
                <Card
                  key={item.name}
                  className="group bg-neutral-900 border-neutral-800 transition cursor-pointer hover:shadow-[0_0_35px_rgba(255,0,0,0.6)]"
                >
                  <CardContent className="p-6">

                    <div className="aspect-square bg-neutral-800 rounded-xl mb-6 overflow-hidden relative">

                      <motion.img
                        src={item.image}
                        alt={item.name}
                        className="object-cover w-full h-full"
                        whileHover={{ scale: 1.1 }}
                        transition={{ duration: 0.4 }}
                        style={{ filter: "drop-shadow(0 0 20px rgba(255,0,0,0.8))" }}
                      />

                    </div>

                    <h3 className="text-xl text-white font-semibold">{item.name}</h3>

                    <div className="flex gap-3 mt-4">
                      <Button
                        className="flex-1"
                        onClick={() => setQuickView(item)}
                      >
                        Quick View
                      </Button>

                      <Button
                        variant="outline"
                        className="flex-1"
                        onClick={() => window.open("https://zmileymerch.printify.me/", "_blank")}
                      >
                        Shop
                      </Button>
                    </div>

                  </CardContent>
                </Card>
              ))}

            </div>

            <Button
              className="text-lg px-12 py-6"
              onClick={() => window.open("https://zmileymerch.printify.me/", "_blank")}
            >
              Visit the Official Merch Store
            </Button>

          </div>

        </section>

        {/* QUICK VIEW */}
        {quickView && (
          <div className="fixed inset-0 bg-black/80 z-50 flex items-center justify-center p-6">
            <div className="bg-neutral-900 rounded-2xl max-w-lg w-full p-6 relative">

              <button
                onClick={() => setQuickView(null)}
                className="absolute top-4 right-4 text-gray-400 hover:text-white"
              >
                <X />
              </button>

              <img
                src={quickView.image}
                alt={quickView.name}
                className="rounded-xl mb-6"
              />

              <h3 className="text-2xl font-bold mb-4">{quickView.name}</h3>

              <Button
                className="w-full"
                onClick={() => window.open("https://zmileymerch.printify.me/", "_blank")}
              >
                View In Store
              </Button>

            </div>
          </div>
        )}

        {/* COMMUNITY */}
        <section id="community" className="px-6 py-32 text-center">

          <Mail className="mx-auto mb-6" size={44}/>

          <h2 className="text-4xl md:text-5xl font-bold">Join the Zmiley Community</h2>

          <p className="text-gray-400 mt-6 max-w-xl mx-auto">
            Early music releases, exclusive merch drops, and behind-the-scenes content.
          </p>

          <div className="mt-10 flex flex-col md:flex-row justify-center gap-4">
            <Input
              value={email}
              onChange={(e)=>setEmail(e.target.value)}
              placeholder="Enter your email"
              className="max-w-xs"
            />
            <Button>Subscribe</Button>
          </div>

        </section>

        {/* SOCIAL */}
        <section className="py-20 text-center bg-neutral-950">

          <h3 className="text-2xl mb-8">Follow Zmiley</h3>

          <div className="flex flex-wrap justify-center gap-8 text-gray-400">

            <a href="https://www.instagram.com/zmiley95?igsh=MWRhcHRoajBndHprZA==" target="_blank" rel="noreferrer">
              <Instagram size={28} className="hover:text-white" />
            </a>

            <a href="https://youtube.com/@zmiley95?si=ceHQzzm5Yi0191LX" target="_blank" rel="noreferrer">
              <Youtube size={28} className="hover:text-white" />
            </a>

            <a href="https://www.tiktok.com/@z.miley?is_from_webapp=1&sender_device=pc" target="_blank" rel="noreferrer">
              <Music size={28} className="hover:text-white" />
            </a>

            <a href="https://www.facebook.com/share/185oTsWe2w/" target="_blank" rel="noreferrer">
              <Facebook size={28} className="hover:text-white" />
            </a>

          </div>

        </section>

        {/* FOOTER */}
        <footer className="text-center py-10 text-gray-500 border-t border-neutral-900">
          zmileyofficial.com • © {new Date().getFullYear()} Zmiley Official
        </footer>

      </div>
    </>
  );
}
