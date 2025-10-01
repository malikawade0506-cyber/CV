import React, { useState } from "react";
import {
  ResponsiveContainer,
  Tooltip,
  Legend,
  // Radial (dashboard)
  RadialBarChart,
  RadialBar,
  // Pie (formations)
  PieChart,
  Pie,
  Cell,
  // Bar (langues)
  BarChart,
  Bar,
  XAxis,
  YAxis,
  CartesianGrid,
  LabelList,
} from "recharts";

// WMS-style interactive CV component — white theme (v3)
export default function WMSCv() {
  const [section, setSection] = useState("dashboard");

  // KPI summary
  const kpis = {
    role: "Malika Wade — M1 Commerce International",
    workYears: 5,
    internshipMonths: 4,
    countries: 2,
    cities: 4,
    target: "Stage 2–6 mois · Paris · Supply Chain & Achats",
    availability: "Disponible à partir de début avril.",
  };

  // Contact / header card
  const contact = {
    name: "Malika Wade",
    email: "malikawade0506@gmail.com",
    phone: "+33 7 84 68 55 17",
    location: "31400 TOULOUSE",
    linkedin: "www.linkedin.com/in/malika-w-235057301",
  };

  // Languages (0–100)
  const languages = [
    { name: "Français", value: 100 },
    { name: "Anglais", value: 100 },
    { name: "Chinois", value: 80 },
    { name: "Sango", value: 85 },
  ];

  const LANG_COLORS = {
    Français: "#0ea5e9", // sky
    Anglais: "#10b981", // emerald
    Chinois: "#f59e0b", // amber
    Sango: "#8b5cf6", // violet
  } as const;

  // Tools
  const tools = [
    { name: "Salesforce", value: 90 },
    { name: "Pipedrive", value: 85 },
    { name: "Excel", value: 90 },
    { name: "HubSpot", value: 70 },
    { name: "Zendesk", value: 65 },
  ];

  // Experiences
  const experiences = [
    {
      id: "manda",
      title: "Manda — Business Developer (Proptech)",
      period: "Puteaux · Stage/Job",
      skills: {
        purchasing: 10,
        logistics: 20,
        crm: 90,
        analysis: 70,
        negotiation: 80,
        comm: 85,
        clientRel: 80,
        teamwork: 75,
        market: 60,
        project: 40,
      },
      note: "Gestion administrative, prospection, CRM intensif.",
    },
    {
      id: "hudsons",
      title: "Hudson's Bay — Customer Service (Montréal)",
      period: "Montréal · Retail",
      skills: {
        purchasing: 0,
        logistics: 0,
        crm: 85,
        analysis: 30,
        negotiation: 60,
        comm: 85,
        clientRel: 90,
        teamwork: 75,
        market: 20,
        project: 20,
      },
      note: "Service client bilingue — pas de pilotage flux ni achats.",
    },
    {
      id: "manege",
      title: "Manège à Bijoux — Vendeuse (Saint-Orens)",
      period: "France · Retail",
      skills: {
        purchasing: 40,
        logistics: 60,
        crm: 70,
        analysis: 30,
        negotiation: 55,
        comm: 70,
        clientRel: 80,
        teamwork: 60,
        market: 0,
        project: 30,
      },
      note: "Pilotage des flux en fin de semestre et rachat de stocks. Pas de veille concurrentielle.",
    },
  ];

  // Education
  const educations = [
    {
      id: "bac",
      title: "Baccalauréat S (2020)",
      totalCourses: 6,
      slices: [
        { name: "SVT", value: 40 },
        { name: "Maths", value: 25 },
        { name: "Physique", value: 20 },
        { name: "Langues", value: 15 },
      ],
    },
    {
      id: "licence",
      title: "Licence LEA — Commerce International (Toulouse, 2020–2025)",
      totalCourses: 12,
      slices: [
        { name: "Études de marché", value: 20 },
        { name: "Marketing digital", value: 15 },
        { name: "Achats", value: 15 },
        { name: "Droit commercial", value: 10 },
        { name: "Prospection", value: 15 },
        { name: "Stats & SI", value: 15 },
        { name: "Communication", value: 10 },
      ],
    },
    {
      id: "master",
      title: "Master — Commerce International (M1, 2024–2026)",
      totalCourses: 8,
      slices: [
        { name: "Business English", value: 10 },
        { name: "Business Development", value: 20 },
        { name: "Achats internationaux", value: 20 },
        { name: "Logistique internationale", value: 20 },
        { name: "Négociation", value: 15 },
        { name: "Douanes & Paiements", value: 15 },
      ],
    },
  ];

  const COLORS = ["#0ea5e9", "#10b981", "#f59e0b", "#ef4444", "#8b5cf6", "#14b8a6", "#eab308"]; // sky, emerald, amber, red, violet, teal, yellow

  // Derived for dashboard radial
  const languagesForRadial = languages.map((l) => ({ ...l, fill: LANG_COLORS[l.name] }));

  return (
    <div className="min-h-screen bg-white text-slate-900 font-sans">
      <div className="max-w-6xl mx-auto p-6 grid grid-cols-12 gap-6">
        {/* Sidebar */}
        <aside className="col-span-3 bg-slate-100 rounded-2xl p-4 shadow-sm border border-slate-200">
          <div className="mb-6 px-2">
            <div className="h-12 w-12 rounded bg-slate-200 flex items-center justify-center font-bold text-slate-700">WMS</div>
            <div className="mt-4 text-sm text-slate-600">Prototype — WMS CV</div>
          </div>
          <nav className="mt-6 space-y-2" aria-label="Sections du CV">
            {[
              { key: "dashboard", label: "Dashboard", icon: "📊" },
              { key: "experiences", label: "Expériences", icon: "💼" },
              { key: "formations", label: "Formations", icon: "🎓" },
              { key: "competences", label: "Compétences", icon: "🛠️" },
              { key: "langues", label: "Langues", icon: "🌐" },
              { key: "outils", label: "Outils", icon: "💻" },
              { key: "interets", label: "Centres d'intérêt", icon: "⭐" },
            ].map((m) => (
              <button
                key={m.key}
                onClick={() => setSection(m.key)}
                className={`w-full text-left flex items-center gap-3 px-3 py-2 rounded-lg hover:bg-slate-200 transition border border-transparent ${
                  section === m.key ? "bg-gradient-to-r from-emerald-100 to-sky-100 border-emerald-200" : ""
                }`}
                aria-current={section === m.key ? "page" : undefined}
              >
                <span className="text-xl" aria-hidden>{m.icon}</span>
                <span className="text-sm">{m.label}</span>
              </button>
            ))}
          </nav>

          <div className="mt-8 text-xs text-slate-600">
            <div className="mb-2 font-medium text-slate-700">KPI rapide</div>
            <div className="grid grid-cols-2 gap-2">
              <div className="bg-white border border-slate-200 p-2 rounded">Exp: <strong>{kpis.workYears}a</strong></div>
              <div className="bg-white border border-slate-200 p-2 rounded">Stage: <strong>{kpis.internshipMonths}m</strong></div>
              <div className="bg-white border border-slate-200 p-2 rounded">Pays: <strong>{kpis.countries}</strong></div>
              <div className="bg-white border border-slate-200 p-2 rounded">Villes: <strong>{kpis.cities}</strong></div>
            </div>
          </div>
        </aside>

        {/* Main */}
        <main className="col-span-9 bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
          {section === "dashboard" && (
            <section>
              <header className="flex items-start justify-between mb-6">
                <div>
                  <h1 className="text-2xl font-semibold">{kpis.role}</h1>
                  <div className="text-sm text-slate-600 mt-1">{kpis.target}</div>
                  <div className="text-sm mt-2 font-medium text-emerald-700">{kpis.availability}</div>
                </div>
                <div className="text-sm text-slate-500">Prototype interactif — style WMS</div>
              </header>

              <div className="grid grid-cols-3 gap-4">
                <div className="col-span-2 bg-slate-50 rounded p-4 border border-slate-200">
                  <h3 className="text-sm text-slate-600 mb-3">Résumé KPI</h3>
                  <div className="grid grid-cols-3 gap-4">
                    <div className="p-3 bg-white border border-slate-200 rounded">
                      <div className="text-xs text-slate-500">Expérience</div>
                      <div className="text-2xl font-bold">{kpis.workYears} ans</div>
                    </div>
                    <div className="p-3 bg-white border border-slate-200 rounded">
                      <div className="text-xs text-slate-500">Stage</div>
                      <div className="text-2xl font-bold">{kpis.internshipMonths} mois</div>
                    </div>
                    <div className="p-3 bg-white border border-slate-200 rounded">
                      <div className="text-xs text-slate-500">Mobilité</div>
                      <div className="text-2xl font-bold">{kpis.countries} pays / {kpis.cities} villes</div>
                    </div>
                  </div>

                  <div className="mt-6">
                    <h4 className="text-sm text-slate-600 mb-2">Top compétences (aperçu)</h4>
                    <div className="space-y-3">
                      {[
                        ["CRM & gestion commerciale", 90],
                        ["Communication", 85],
                        ["Négociation", 80],
                        ["Analyse & reporting", 70],
                        ["Gestion achats", 40],
                      ].map(([label, val]) => (
                        <div key={label}>
                          <div className="flex justify-between text-xs text-slate-600 mb-1">
                            <span>{label}</span>
                            <span>{val}%</span>
                          </div>
                          <div className="w-full h-2 bg-slate-200 rounded">
                            <div style={{ width: `${val}%` }} className="h-2 bg-emerald-500 rounded" />
                          </div>
                        </div>
                      ))}
                    </div>
                  </div>
                </div>

                <div className="bg-slate-50 rounded p-4 border border-slate-200">
                  <h3 className="text-sm text-slate-600 mb-3">Langues (A1→C2)</h3>
                  <div style={{ height: 220 }}>
                    <ResponsiveContainer width="100%" height={220}>
                      <RadialBarChart innerRadius="10%" outerRadius="100%" data={languagesForRadial} startAngle={180} endAngle={-180}>
                        <RadialBar minAngle={15} background clockWise dataKey="value" />
                        <Tooltip formatter={(v) => `${v}%`} />
                        <Legend />
                      </RadialBarChart>
                    </ResponsiveContainer>
                  </div>
                </div>
              </div>

              <div className="mt-6 grid grid-cols-3 gap-4">
                <div className="col-span-2 bg-slate-50 rounded p-4 border border-slate-200">
                  <h4 className="text-sm text-slate-600 mb-3">Profil synthèse</h4>
                  <p className="text-sm text-slate-700">Étudiante en Master Commerce International — expérience cross-country, forte maîtrise des outils CRM et expérience en prospection / business development. Recherche un stage de 2 à 6 mois à Paris en Supply Chain & Achats.</p>
                </div>
                <div className="bg-slate-50 rounded p-4 border border-slate-200">
                  <h4 className="text-sm text-slate-600 mb-3">Contact</h4>
                  <ul className="text-sm text-slate-700 space-y-1">
                    <li><strong>{contact.name}</strong></li>
                    <li><a className="underline" href={`mailto:${contact.email}`}>{contact.email}</a></li>
                    <li><a className="underline" href={`tel:${contact.phone.replace(/\s/g, "")}`}>{contact.phone}</a></li>
                    <li>{contact.location}</li>
                    <li><a className="underline" href={`https://${contact.linkedin}`} target="_blank" rel="noreferrer">{contact.linkedin}</a></li>
                    <li><a className="underline" href={`https://${contact.portfolio}`} target="_blank" rel="noreferrer">{contact.portfolio}</a></li>
                  </ul>
                </div>
              </div>
            </section>
          )}

          {section === "experiences" && (
            <section>
              <h2 className="text-xl font-semibold mb-4">Expériences professionnelles</h2>
              <div className="space-y-4">
                {experiences.map((exp) => (
                  <div key={exp.id} className="bg-slate-50 rounded p-4 border border-slate-200">
                    <div className="flex items-center justify-between mb-2">
                      <div>
                        <div className="text-sm text-slate-500">{exp.period}</div>
                        <div className="text-lg font-medium">{exp.title}</div>
                      </div>
                      <div className="text-sm text-slate-500">Détail des compétences</div>
                    </div>

                    <div className="grid grid-cols-2 gap-4">
                      <div>
                        {Object.entries(exp.skills).map(([k, v]) => (
                          <div key={k} className="mb-2">
                            <div className="flex justify-between text-xs text-slate-600 mb-1 capitalize">
                              <span>{k.replace(/([A-Z])/g, " $1")}</span>
                              <span>{v}%</span>
                            </div>
                            <div className="w-full h-2 bg-white border border-slate-200 rounded">
                              <div style={{ width: `${v}%` }} className="h-2 bg-sky-500 rounded" />
                            </div>
                          </div>
                        ))}
                      </div>
                      <div>
                        <div className="text-sm text-slate-600 mb-2">Notes</div>
                        <div className="text-sm text-slate-700">{exp.note}</div>
                      </div>
                    </div>
                  </div>
                ))}
              </div>
            </section>
          )}

          {section === "formations" && (
            <section>
              <h2 className="text-xl font-semibold mb-4">Formations</h2>
              <div className="grid grid-cols-3 gap-4">
                {educations.map((edu) => (
                  <div key={edu.id} className="bg-slate-50 rounded p-4 border border-slate-200">
                    <div className="flex items-center justify-between mb-3">
                      <div>
                        <div className="text-sm text-slate-500">{edu.totalCourses} cours</div>
                        <div className="text-lg font-medium">{edu.title}</div>
                      </div>
                      <div className="text-xs text-slate-500">Diagramme de connaissances</div>
                    </div>

                    <div style={{ height: 180 }}>
                      <ResponsiveContainer width="100%" height={180}>
                        <PieChart>
                          <Pie data={edu.slices} dataKey="value" outerRadius={70} innerRadius={35}>
                            {edu.slices.map((entry, idx) => (
                              <Cell key={`cell-${idx}`} fill={COLORS[idx % COLORS.length]} />
                            ))}
                          </Pie>
                          <Tooltip formatter={(v) => `${v}%`} />
                        </PieChart>
                      </ResponsiveContainer>
                    </div>

                    <div className="mt-3 text-xs text-slate-600">
                      {edu.slices.map((s, idx) => (
                        <div key={s.name} className="flex items-center gap-2 mb-1">
                          <div className="w-3 h-3 rounded" style={{ background: COLORS[idx % COLORS.length] }} />
                          <div className="flex-1">{s.name} — {s.value}%</div>
                        </div>
                      ))}
                    </div>

                    <details className="mt-3 text-xs text-slate-600">
                      <summary className="cursor-pointer select-none">Détails des cours</summary>
                      <div className="mt-2 text-xs leading-snug">
                        {edu.id === "licence" && (
                          <div>
                            <p className="mb-1">Études de marché : théorie marketing (10h) — notions méthodologiques, études qualitatives/quantitatives.</p>
                            <p className="mb-1">Études de marché : outils informatiques (10h) — mise en pratique avec SPSS/Sphinx.</p>
                            <p className="mb-1">Introduction au marketing digital (20h) — CMS, mailing, réseaux sociaux, SaaS.</p>
                            <p className="mb-1">Achats (20h) — méthodes d'analyse, gestion des stocks, sélection fournisseurs.</p>
                            <p className="mb-1">Droit commercial (24h), Prospection (20h), Statistiques appliquées (14h), SI comptable (14h), Gestion de projet (12h), Communication (20h).</p>
                          </div>
                        )}
                        {edu.id === "master" && (
                          <div>
                            <p className="mb-1">UE 701 — Business English; UE 703 — Business Development; UE 706 — Achats internationaux; UE 805 — Logistique internationale; Négociation, Douanes, Paiements.</p>
                          </div>
                        )}
                        {edu.id === "bac" && (
                          <div>
                            <p className="mb-1">Baccalauréat scientifique — parcours SVT et sciences fondamentales.</p>
                          </div>
                        )}
                      </div>
                    </details>
                  </div>
                ))}
              </div>
            </section>
          )}

          {section === "competences" && (
            <section>
              <h2 className="text-xl font-semibold mb-4">Compétences (détaillées)</h2>
              <div className="grid grid-cols-2 gap-4">
                <div className="bg-slate-50 rounded p-4 border border-slate-200">
                  <h3 className="text-sm text-slate-600 mb-3">Compétences transverses</h3>
                  {[
                    "Gestion des achats / approvisionnement",
                    "Pilotage des flux logistiques",
                    "CRM et outils de gestion commerciale",
                    "Analyse de données et reporting",
                    "Négociation commerciale",
                    "Communication orale et écrite",
                    "Gestion de la relation client",
                    "Travail en équipe et collaboration",
                    "Connaissance du marché et veille concurrentielle",
                    "Gestion de projet et organisation",
                  ].map((c, idx) => (
                    <div key={c} className="mb-3">
                      <div className="flex justify-between text-xs text-slate-600 mb-1">
                        <span>{c}</span>
                        <span>{[90,60,90,70,80,85,80,75,60,50][idx]}%</span>
                      </div>
                      <div className="w-full h-2 bg-slate-200 rounded">
                        <div style={{ width: `${[90,60,90,70,80,85,80,75,60,50][idx]}%` }} className="h-2 bg-emerald-500 rounded" />
                      </div>
                    </div>
                  ))}
                </div>
                <div className="bg-slate-50 rounded p-4 border border-slate-200">
                  <h3 className="text-sm text-slate-600 mb-3">Outils / Digital</h3>
                  {tools.map((t) => (
                    <div key={t.name} className="mb-3">
                      <div className="flex justify-between text-xs text-slate-600 mb-1">
                        <span>{t.name}</span>
                        <span>{t.value}%</span>
                      </div>
                      <div className="w-full h-2 bg-slate-200 rounded">
                        <div style={{ width: `${t.value}%` }} className="h-2 bg-sky-500 rounded" />
                      </div>
                    </div>
                  ))}
                </div>
              </div>
            </section>
          )}

          {section === "langues" && (
            <section>
              <h2 className="text-xl font-semibold mb-4">Langues</h2>
              <div className="bg-slate-50 rounded p-4 border border-slate-200">
                <div style={{ height: 260 }}>
                  <ResponsiveContainer width="100%" height={260}>
                    <BarChart data={languages} layout="vertical" margin={{ left: 12, right: 8, top: 8, bottom: 8 }}>
                      <CartesianGrid strokeDasharray="3 3" />
                      <XAxis type="number" domain={[0, 100]} hide />
                      <YAxis dataKey="name" type="category" width={110} />
                      <Tooltip formatter={(v) => `${v}%`} />
                      <Bar dataKey="value" radius={[6, 6, 6, 6]}>
                        {languages.map((L) => (
                          <Cell key={L.name} fill={LANG_COLORS[L.name]} />
                        ))}
                        <LabelList dataKey="value" position="right" formatter={(v) => `${v}%`} />
                      </Bar>
                    </BarChart>
                  </ResponsiveContainer>
                </div>
              </div>
            </section>
          )}

          {section === "outils" && (
            <section>
              <h2 className="text-xl font-semibold mb-4">Outils numériques</h2>
              <div className="grid grid-cols-3 gap-4">
                {tools.map((t) => (
                  <div key={t.name} className="bg-slate-50 rounded p-4 border border-slate-200">
                    <div className="flex items-baseline justify-between mb-3">
                      <div className="text-sm">{t.name}</div>
                      <div className="text-lg font-bold">{t.value}%</div>
                    </div>
                    <div className="w-full h-2 bg-slate-200 rounded">
                      <div style={{ width: `${t.value}%` }} className="h-2 bg-emerald-500 rounded" />
                    </div>
                  </div>
                ))}
              </div>
            </section>
          )}

          {section === "interets" && (
            <section>
              <h2 className="text-xl font-semibold mb-4">Centres d'intérêt</h2>
              <ul className="list-disc pl-6 text-slate-700 space-y-1">
                <li>Dessin</li>
                <li>Photographie</li>
                <li>Pâtisserie</li>
                <li>Cuisine</li>
              </ul>
            </section>
          )}
        </main>
      </div>
    </div>
  );
}
