# GUIDE-DIGITAL-EARTH-AFRICA-
Permet de comprendre les codes d'acquisition 
import { useState } from "react";

const pages = [
  {
    id: "intro",
    num: "01",
    title: "Présentation",
    subtitle: "Digital Earth Africa",
    icon: "🌍",
    color: "#0055A5",
    accent: "#2A9FD6",
  },
  {
    id: "sandbox",
    num: "02",
    title: "Sandbox & Accès",
    subtitle: "JupyterHub Cloud",
    icon: "☁️",
    color: "#006B3C",
    accent: "#27AE60",
  },
  {
    id: "catalogue",
    num: "03",
    title: "Catalogue",
    subtitle: "Données Disponibles",
    icon: "🛰️",
    color: "#7B2D8B",
    accent: "#A855F7",
  },
  {
    id: "odc",
    num: "04",
    title: "Acquisition ODC",
    subtitle: "dc.load() Python",
    icon: "⚙️",
    color: "#B45309",
    accent: "#F59E0B",
  },
  {
    id: "ard",
    num: "05",
    title: "Produits ARD",
    subtitle: "Indices Spectraux",
    icon: "📡",
    color: "#0E7490",
    accent: "#22D3EE",
  },
  {
    id: "exercice",
    num: "06",
    title: "Exercice Pratique",
    subtitle: "NDVI Guide Complet",
    icon: "🧪",
    color: "#BE185D",
    accent: "#F472B6",
  },
];

const CodeBlock = ({ lines }) => (
  <div style={{
    background: "#0D1117",
    borderRadius: 10,
    padding: "14px 18px",
    fontFamily: "'Courier New', monospace",
    fontSize: 12.5,
    lineHeight: 1.7,
    overflowX: "auto",
    border: "1px solid #30363D",
    boxShadow: "inset 0 2px 8px rgba(0,0,0,0.3)"
  }}>
    {lines.map((line, i) => {
      const isComment = line.trim().startsWith("#");
      const isBlank = line.trim() === "";
      let color = "#E6EDF3";
      if (isComment) color = "#8B949E";
      else if (line.includes("dc.load") || line.includes("datacube") || line.includes("def ")) color = "#79C0FF";
      else if (line.includes("'") || line.includes('"')) color = "#A5D6FF";
      else if (line.match(/^\s*(import|from|return|print)/)) color = "#FF7B72";
      return (
        <div key={i} style={{ color, minHeight: isBlank ? 8 : undefined }}>
          <span style={{ color: "#484F58", userSelect: "none", marginRight: 12, fontSize: 11 }}>
            {String(i + 1).padStart(2, " ")}
          </span>
          {line}
        </div>
      );
    })}
  </div>
);

const Tag = ({ text, color = "#2A9FD6" }) => (
  <span style={{
    background: color + "22",
    color: color,
    border: `1px solid ${color}44`,
    borderRadius: 6,
    padding: "2px 9px",
    fontSize: 11,
    fontWeight: 700,
    letterSpacing: 0.4,
    fontFamily: "monospace"
  }}>{text}</span>
);

const DataTable = ({ headers, rows, colors: c }) => (
  <div style={{ overflowX: "auto" }}>
    <table style={{ width: "100%", borderCollapse: "collapse", fontSize: 12.5 }}>
      <thead>
        <tr>
          {headers.map((h, i) => (
            <th key={i} style={{
              background: c.header, color: "#fff",
              padding: "8px 12px", textAlign: "left",
              fontWeight: 700, fontSize: 11.5, letterSpacing: 0.3
            }}>{h}</th>
          ))}
        </tr>
      </thead>
      <tbody>
        {rows.map((row, i) => (
          <tr key={i} style={{ background: i % 2 === 0 ? "#fff" : c.alt }}>
            {row.map((cell, j) => (
              <td key={j} style={{
                padding: "7px 12px", borderBottom: `1px solid ${c.border}`,
                color: "#1e293b", lineHeight: 1.5
              }}
                dangerouslySetInnerHTML={{ __html: cell }} />
            ))}
          </tr>
        ))}
      </tbody>
    </table>
  </div>
);

const TipBox = ({ icon, label, text, color }) => (
  <div style={{
    display: "flex", gap: 12, alignItems: "flex-start",
    background: color + "11", border: `1px solid ${color}44`,
    borderLeft: `4px solid ${color}`,
    borderRadius: 8, padding: "10px 14px", marginTop: 10
  }}>
    <span style={{ fontSize: 18, flexShrink: 0 }}>{icon}</span>
    <div>
      <div style={{ fontWeight: 700, color: color, fontSize: 12.5, marginBottom: 3 }}>{label}</div>
      <div style={{ fontSize: 12, color: "#475569", lineHeight: 1.6 }}>{text}</div>
    </div>
  </div>
);

const StepList = ({ steps, accent }) => (
  <div style={{ display: "flex", flexDirection: "column", gap: 8 }}>
    {steps.map((step, i) => (
      <div key={i} style={{ display: "flex", gap: 12, alignItems: "flex-start" }}>
        <div style={{
          width: 26, height: 26, borderRadius: "50%", background: accent,
          color: "#fff", fontWeight: 800, fontSize: 12,
          display: "flex", alignItems: "center", justifyContent: "center", flexShrink: 0, marginTop: 1
        }}>{i + 1}</div>
        <div>
          <div style={{ fontWeight: 700, color: "#1e293b", fontSize: 13 }}>{step.title}</div>
          <div style={{ fontSize: 12, color: "#64748b", lineHeight: 1.5, marginTop: 2 }}>{step.desc}</div>
        </div>
      </div>
    ))}
  </div>
);

// ── PAGE CONTENTS ────────────────────────────────────────────────

function PageIntro({ c }) {
  return (
    <div>
      <p style={{ color: "#475569", lineHeight: 1.7, marginBottom: 16, fontSize: 13.5 }}>
        <strong>Digital Earth Africa (DE Africa)</strong> est une plateforme d'observation de la Terre
        financée par le G7 et gérée sous l'égide de l'Union Africaine. Elle met à disposition des
        données satellitaires <strong>gratuites</strong> sur l'ensemble du continent africain via un
        environnement cloud JupyterHub basé sur l'<strong>Open Data Cube (ODC)</strong>.
      </p>

      <div style={{ display: "grid", gridTemplateColumns: "repeat(3, 1fr)", gap: 10, marginBottom: 20 }}>
        {[
          ["🗓", "Lancé en 2019", "Soutenu par le G7"],
          ["🌍", "Afrique entière", "Couverture continentale"],
          ["💰", "100% Gratuit", "Aucune licence requise"],
          ["🛰", "Landsat + Sentinel", "ALOS, SRTM et plus"],
          ["📅", "Depuis 1984", "Archive historique longue"],
          ["🐍", "Python ODC", "JupyterHub cloud"],
        ].map(([icon, title, sub], i) => (
          <div key={i} style={{
            background: "#F8FAFC", border: "1px solid #E2E8F0",
            borderRadius: 10, padding: "12px 14px", textAlign: "center"
          }}>
            <div style={{ fontSize: 22, marginBottom: 4 }}>{icon}</div>
            <div style={{ fontWeight: 700, color: "#1e293b", fontSize: 12.5 }}>{title}</div>
            <div style={{ color: "#94A3B8", fontSize: 11.5 }}>{sub}</div>
          </div>
        ))}
      </div>

      <h3 style={{ color: c.color, fontSize: 14, fontWeight: 700, marginBottom: 10 }}>Cas d'usage principaux</h3>
      <div style={{ display: "grid", gridTemplateColumns: "repeat(2, 1fr)", gap: 8 }}>
        {[
          ["🌱", "Agriculture", "Suivi des cultures, NDVI, sécurité alimentaire"],
          ["💧", "Ressources en eau", "Cartographie lacs, inondations, WOfS"],
          ["🌲", "Forêts", "Déforestation, couverture végétale SAR"],
          ["🏙️", "Urbanisation", "Extension urbaine, artificialisation des sols"],
          ["🌊", "Littoral", "Évolution du trait de côte, mangroves"],
          ["🌡️", "Climat", "Sécheresse, précipitations, anomalies"],
        ].map(([icon, title, desc], i) => (
          <div key={i} style={{
            display: "flex", gap: 10, padding: "10px 12px",
            background: c.accent + "0D", border: `1px solid ${c.accent}33`,
            borderRadius: 8, alignItems: "flex-start"
          }}>
            <span style={{ fontSize: 18 }}>{icon}</span>
            <div>
              <div style={{ fontWeight: 700, color: "#1e293b", fontSize: 12.5 }}>{title}</div>
              <div style={{ color: "#64748b", fontSize: 11.5 }}>{desc}</div>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}

function PageSandbox({ c }) {
  return (
    <div>
      <p style={{ color: "#475569", lineHeight: 1.7, marginBottom: 16, fontSize: 13.5 }}>
        Le <strong>Sandbox DE Africa</strong> est un JupyterHub entièrement géré dans le cloud.
        Il permet d'exécuter des analyses Python directement sur les données, sans téléchargement local.
      </p>

      <h3 style={{ color: c.color, fontSize: 14, fontWeight: 700, marginBottom: 10 }}>Accès et démarrage</h3>
      <StepList accent={c.accent} steps={[
        { title: "Inscription", desc: "Aller sur sandbox.digitalearth.africa → cliquer 'Sign Up' → remplir le formulaire email" },
        { title: "Confirmation", desc: "Confirmer votre adresse email. Le compte est approuvé automatiquement sous quelques minutes." },
        { title: "Connexion", desc: "Cliquer 'Sign In' → choisir la taille serveur : Small (2 CPU, 8 Go RAM) pour débuter." },
        { title: "Démarrage", desc: "Le serveur JupyterHub démarre en 1-2 minutes. Environnement Python pré-configuré prêt." },
        { title: "Explorer", desc: "Le dossier /notebooks/ contient des dizaines d'exemples officiels classés par thème." },
      ]} />

      <h3 style={{ color: c.color, fontSize: 14, fontWeight: 700, margin: "18px 0 10px" }}>Librairies pré-installées</h3>
      <DataTable
        headers={["Librairie", "Rôle", "Import"]}
        rows={[
          ["<strong>datacube</strong>", "Accès au catalogue ODC et chargement des données", "<code>import datacube</code>"],
          ["<strong>xarray</strong>", "Tableaux N-dim spatio-temporels avec métadonnées", "<code>import xarray as xr</code>"],
          ["<strong>numpy</strong>", "Calculs matriciels et traitement numérique", "<code>import numpy as np</code>"],
          ["<strong>geopandas</strong>", "Manipulation de données vecteur (shapefiles, gpkg)", "<code>import geopandas as gpd</code>"],
          ["<strong>deafrica_tools</strong>", "Utilitaires DE Africa (rgb, display_map, masques)", "<code>from deafrica_tools.plotting import rgb</code>"],
          ["<strong>rioxarray</strong>", "Lecture/écriture GeoTIFF avec projection", "<code>import rioxarray</code>"],
        ]}
        colors={{ header: c.color, alt: "#F0FDF4", border: "#D1FAE5" }}
      />
      <TipBox icon="💾" label="Persistance des données"
        text="Seul le dossier /home/user/ est persistant entre les sessions. Sauvegarder vos notebooks et résultats dans ce dossier. /tmp/ est effacé à chaque arrêt du serveur."
        color={c.accent} />
    </div>
  );
}

function PageCatalogue({ c }) {
  return (
    <div>
      <p style={{ color: "#475569", lineHeight: 1.7, marginBottom: 16, fontSize: 13.5 }}>
        Toutes les données sont disponibles au niveau <strong>ARD (Analysis Ready Data)</strong> :
        corrigées atmosphériquement et géométriquement, prêtes à l'analyse directe.
      </p>

      <h3 style={{ color: c.color, fontSize: 14, fontWeight: 700, marginBottom: 10 }}>Données Optiques</h3>
      <DataTable
        headers={["Satellite", "Identifiant ODC", "Résolution", "Cadence", "Archive"]}
        rows={[
          ["Landsat 5 SR", "<code>ls5_sr</code>", "30 m", "16 jours", "1984"],
          ["Landsat 7 SR", "<code>ls7_sr</code>", "30 m", "16 jours", "1999"],
          ["Landsat 8/9 SR", "<code>ls8_sr / ls9_sr</code>", "30 m", "16 jours", "2013"],
          ["Sentinel-2 L2A", "<code>s2_l2a</code>", "10/20/60 m", "5 jours", "2017"],
          ["GeoMAD Landsat", "<code>ls_geomedian</code>", "30 m", "Annuel", "1984"],
          ["GeoMAD Sentinel-2", "<code>s2_geomedian</code>", "10 m", "Annuel", "2017"],
        ]}
        colors={{ header: c.color, alt: "#FAF5FF", border: "#E9D5FF" }}
      />

      <h3 style={{ color: c.color, fontSize: 14, fontWeight: 700, margin: "16px 0 10px" }}>Données Radar & Thématiques</h3>
      <DataTable
        headers={["Produit", "Identifiant ODC", "Résolution", "Utilisation"]}
        rows={[
          ["Sentinel-1 SAR (VV/VH)", "<code>s1_rtc</code>", "10-20 m", "Inondations, végétation, urbain"],
          ["ALOS/PALSAR-2 SAR", "<code>alos_palsar_mosaic</code>", "25 m", "Forêts, zones humides"],
          ["SRTM DEM (MNT)", "<code>srtm</code>", "30 m", "Altimétrie, pentes, bassins"],
          ["Water Obs. (WOfS)", "<code>wofs_ls</code>", "30 m", "Eau de surface historique"],
          ["Fractional Cover", "<code>fc_ls</code>", "30 m", "Végétation verte/sèche/sol nu"],
          ["Cropland Extent", "<code>crop_mask_africa</code>", "10 m", "Zones agricoles africaines"],
        ]}
        colors={{ header: "#4C1D95", alt: "#FAF5FF", border: "#E9D5FF" }}
      />
      <TipBox icon="🔍" label="Explorer le catalogue"
        text="Commande pour lister tous les produits disponibles dans le Sandbox : dc.list_products()[['name','description']].to_string()  — ou via l'interface web : explorer.digitalearth.africa"
        color={c.accent} />
    </div>
  );
}

function PageODC({ c }) {
  return (
    <div>
      <p style={{ color: "#475569", lineHeight: 1.7, marginBottom: 14, fontSize: 13.5 }}>
        L'<strong>Open Data Cube (ODC)</strong> est le moteur d'accès aux données.
        La fonction <code style={{ background: "#FEF3C7", padding: "1px 6px", borderRadius: 4, color: "#92400E" }}>dc.load()</code> charge
        les données sous forme d'un tableau <strong>xarray.Dataset</strong> multidimensionnel (x, y, time).
      </p>

      <h3 style={{ color: c.color, fontSize: 14, fontWeight: 700, marginBottom: 8 }}>Connexion au Datacube</h3>
      <CodeBlock lines={[
        "import datacube",
        "import numpy as np",
        "import matplotlib.pyplot as plt",
        "from deafrica_tools.plotting import rgb",
        "",
        "# Connexion au datacube DE Africa",
        "dc = datacube.Datacube(app='mon_analyse')",
        "",
        "# Lister les produits disponibles",
        "print(dc.list_products()[['name','description']].head(20))",
      ]} />

      <h3 style={{ color: c.color, fontSize: 14, fontWeight: 700, margin: "16px 0 10px" }}>Paramètres de dc.load()</h3>
      <DataTable
        headers={["Paramètre", "Type", "Description", "Exemple"]}
        rows={[
          ["<code>product</code>", "str", "Nom du produit dans le catalogue", "<code>'s2_l2a'</code>"],
          ["<code>x</code>", "tuple", "Longitude (min, max) en degrés", "<code>(35.5, 36.0)</code>"],
          ["<code>y</code>", "tuple", "Latitude (min, max) en degrés", "<code>(-1.5, -1.0)</code>"],
          ["<code>time</code>", "tuple", "Période temporelle (début, fin)", "<code>('2023-01','2023-12')</code>"],
          ["<code>measurements</code>", "list", "Bandes spectrales à charger", "<code>['red','nir','green']</code>"],
          ["<code>resolution</code>", "tuple", "Résolution en mètres (négatif pour y)", "<code>(-20, 20)</code>"],
          ["<code>output_crs</code>", "str", "Système de coordonnées de sortie", "<code>'EPSG:6933'</code>"],
          ["<code>group_by</code>", "str", "Regroupement temporel des scènes", "<code>'solar_day'</code>"],
          ["<code>dask_chunks</code>", "dict", "Chargement paresseux (grandes zones)", "<code>{'time':1,'x':2048}</code>"],
        ]}
        colors={{ header: c.color, alt: "#FFFBEB", border: "#FDE68A" }}
      />

      <h3 style={{ color: c.color, fontSize: 14, fontWeight: 700, margin: "14px 0 8px" }}>Exemple Complet — Lac Victoria</h3>
      <CodeBlock lines={[
        "ds = dc.load(",
        "    product='s2_l2a',",
        "    x=(34.8, 35.2),",
        "    y=(-0.5, -0.1),",
        "    time=('2023-01-01', '2023-06-30'),",
        "    measurements=['red', 'green', 'blue', 'nir'],",
        "    resolution=(-20, 20),",
        "    output_crs='EPSG:6933',",
        "    group_by='solar_day'",
        ")",
        "",
        "print(ds)  # Dataset (time: N, y: M, x: P)",
        "rgb(ds, bands=['red', 'green', 'blue'])  # Affichage couleur naturelle",
      ]} />
      <TipBox icon="⚡" label="Dask pour les grandes zones"
        text="Utiliser dask_chunks pour les grandes étendues ou longues séries. Les données sont chargées en mémoire uniquement lors de l'appel .compute(). Évite les erreurs de mémoire sur les régions étendues."
        color={c.accent} />
    </div>
  );
}

function PageARD({ c }) {
  return (
    <div>
      <p style={{ color: "#475569", lineHeight: 1.7, marginBottom: 14, fontSize: 13.5 }}>
        Les produits <strong>ARD</strong> sont corrigés et prêts à l'emploi.
        <strong> Diviser les valeurs brutes par 10 000</strong> avant tout calcul d'indice pour obtenir la réflectance réelle [0–1].
      </p>

      <div style={{ display: "grid", gridTemplateColumns: "repeat(2, 1fr)", gap: 10, marginBottom: 16 }}>
        {[
          { title: "Landsat SR", id: "ls5_sr / ls8_sr / ls9_sr", bands: "blue, green, red, nir, swir1, swir2, thermal", note: "Corrections LaSRC + Fmask" },
          { title: "Sentinel-2 L2A", id: "s2_l2a", bands: "blue, green, red, red_edge_1/2/3, nir, nir_narrow, swir_1/2", note: "Corrections Sen2Cor + s2cloudless" },
        ].map((item, i) => (
          <div key={i} style={{ background: "#F8FAFC", border: `1px solid ${c.accent}33`, borderRadius: 10, padding: 14 }}>
            <div style={{ fontWeight: 700, color: c.color, fontSize: 13, marginBottom: 6 }}>{item.title}</div>
            <Tag text={item.id} color={c.accent} />
            <div style={{ color: "#64748b", fontSize: 11.5, marginTop: 8, lineHeight: 1.5 }}>
              <strong>Bandes :</strong> {item.bands}
            </div>
            <div style={{ color: "#64748b", fontSize: 11.5, marginTop: 4 }}>
              <strong>Corrections :</strong> {item.note}
            </div>
          </div>
        ))}
      </div>

      <h3 style={{ color: c.color, fontSize: 14, fontWeight: 700, marginBottom: 10 }}>WOfS — Water Observations from Space</h3>
      <DataTable
        headers={["Produit", "Description", "Usage"]}
        rows={[
          ["<code>wofs_ls</code>", "Observation eau par scène Landsat (bit flag)", "Détection inondations ponctuelles"],
          ["<code>wofs_ls_summary_alltime</code>", "% historique de temps avec eau présente", "Zones humides permanentes"],
          ["<code>wofs_ls_summary_annual</code>", "Statistiques eau annuelles (count, frequency)", "Suivi interannuel lacs/réservoirs"],
        ]}
        colors={{ header: "#0E7490", alt: "#ECFEFF", border: "#CFFAFE" }}
      />

      <h3 style={{ color: c.color, fontSize: 14, fontWeight: 700, margin: "14px 0 10px" }}>Indices Spectraux</h3>
      <DataTable
        headers={["Indice", "Formule", "Source", "Utilité"]}
        rows={[
          ["<strong>NDVI</strong>", "(NIR − Red) / (NIR + Red)", "s2_l2a / ls8_sr", "Santé végétation [−1, 1]"],
          ["<strong>NDWI</strong>", "(Green − NIR) / (Green + NIR)", "s2_l2a", "Détection eau de surface"],
          ["<strong>NDBI</strong>", "(SWIR1 − NIR) / (SWIR1 + NIR)", "ls8_sr", "Milieu bâti, urbanisation"],
          ["<strong>EVI</strong>", "2.5×(NIR−R)/(NIR+6R−7.5B+1)", "s2_l2a", "Végétation (corrigé sol/atm)"],
          ["<strong>BSI</strong>", "(SWIR+Red−NIR−Blue) / (somme)", "ls8_sr", "Sol nu, dégradation des terres"],
        ]}
        colors={{ header: c.color, alt: "#ECFEFF", border: "#CFFAFE" }}
      />
      <TipBox icon="📐" label="Normalisation obligatoire"
        text="red = ds.red / 10000  ;  nir = ds.nir / 10000  →  ndvi = (nir - red) / (nir + red)  →  ndvi.mean(dim='time').plot(cmap='RdYlGn', vmin=-0.2, vmax=0.8)"
        color={c.accent} />
    </div>
  );
}

function PageExercice({ c }) {
  const [done, setDone] = useState({});
  const steps = [
    { title: "Définir la zone", desc: "x=(38.0, 38.5), y=(7.5, 8.0) — région d'Arsi, Éthiopie. Vérifier via display_map()" },
    { title: "Charger Sentinel-2", desc: "dc.load(product='s2_l2a', measurements=['red','nir'], resolution=(-20,20), ...)" },
    { title: "Masquer les nuages", desc: "ds_clean = ds.where(ds.oa_fmask == 1)  # Garder uniquement pixels valides" },
    { title: "Normaliser et calculer", desc: "red = ds.red/10000 ; nir = ds.nir/10000 ; ndvi = (nir - red)/(nir + red)" },
    { title: "Agrégation mensuelle", desc: "ndvi_m = ndvi.resample(time='1ME').median('time')  # Médiane sans nuages" },
    { title: "Visualiser", desc: "ndvi_m.plot(col='time', col_wrap=4, cmap='RdYlGn', vmin=-0.2, vmax=0.8)" },
    { title: "E
