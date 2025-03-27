# Powerbi-Portal-Rotativo
import React, { useEffect, useState } from "react";

const dashboards = [
  {
    title: "CD Turismo",
    url: "https://app.powerbi.com/view?r=RELATORIO_1"
  },
  {
    title: "CD Amazonino",
    url: "https://app.powerbi.com/view?r=RELATORIO_2"
  },
  {
    title: "PMPL - Preventiva",
    url: "https://app.powerbi.com/view?r=RELATORIO_3"
  },
  {
    title: "PMOS - Corretiva",
    url: "https://app.powerbi.com/view?r=RELATORIO_4"
  }
];

export default function PowerBIPortalRotativo() {
  const [index, setIndex] = useState(0);

  // Troca automática a cada 30 segundos
  useEffect(() => {
    const interval = setInterval(() => {
      setIndex((prevIndex) => (prevIndex + 1) % dashboards.length);
    }, 30000);
    return () => clearInterval(interval);
  }, []);

  return (
    <div className="h-screen w-screen bg-gray-100 flex flex-col">
      <header className="bg-blue-600 text-white p-4 text-xl font-bold shadow">
        Dashboards Manutenção - Bemol
      </header>
      <main className="flex-1 flex items-center justify-center">
        <iframe
          title={dashboards[index].title}
          src={dashboards[index].url}
          width="100%"
          height="100%"
          className="border-0 w-full h-full"
          allowFullScreen
        ></iframe>
      </main>
      <footer className="text-center p-2 text-sm text-gray-500">
        Exibindo: {dashboards[index].title}
      </footer>
    </div>
  );
}

