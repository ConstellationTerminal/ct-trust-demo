{\rtf1\ansi\ansicpg1252\cocoartf2639
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;\f1\fnil\fcharset0 LucidaGrande;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 import math\
import numpy as np\
import pandas as pd\
import streamlit as st\
\
st.set_page_config(page_title="Trust-as-Capacity Demo (VANU)", layout="wide")\
\
# -----------------------------\
# Core model\
# -----------------------------\
def vanu_delta(work: float, coherence: float, entropy: float, c_min: float, k: float, lam: float) -> float:\
    """Single-step VANU contribution."""\
    if coherence < c_min:\
        return 0.0\
    return float(work) * float(coherence) ** float(k) * math.exp(-float(lam) * float(entropy))\
\
def pta_band(coherence: float, entropy: float) -> str:\
    """\
    Simple, defensible banding (illustrative):\
    - Volatile/Low-binding: low coherence or high entropy\
    - Cooperative/Stabilizing: moderate-high coherence, moderate-low entropy\
    - Deep/High-binding: high coherence, low entropy\
    - Institutional/Field: high coherence sustained + low entropy (in practice: aggregate condition)\
    """\
    if coherence < 0.45 or entropy > 0.7:\
        return "Row I: Volatile / Low-binding"\
    if coherence < 0.75 or entropy > 0.45:\
        return "Row II: Cooperative / Stabilizing"\
    if coherence >= 0.75 and entropy <= 0.25:\
        return "Row III: Deep / High-binding"\
    return "Row II\'96III: Transitional (stabilizing 
\f1 \uc0\u8594 
\f0  deep)"\
\
def generate_sample(n: int, mode: str, seed: int = 7) -> pd.DataFrame:\
    rng = np.random.default_rng(seed)\
    t = np.arange(n)\
\
    if mode == "Noisy (engagement-like)":\
        work = rng.uniform(0.5, 1.2, size=n)\
        coherence = np.clip(rng.normal(0.42, 0.18, size=n), 0, 1)\
        entropy = np.clip(rng.normal(0.65, 0.15, size=n), 0, 1)\
\
    elif mode == "Coherent builder":\
        work = rng.uniform(0.6, 1.1, size=n)\
        coherence = np.clip(rng.normal(0.78, 0.10, size=n), 0, 1)\
        entropy = np.clip(rng.normal(0.22, 0.10, size=n), 0, 1)\
\
    elif mode == "Mixed with shocks":\
        work = rng.uniform(0.6, 1.3, size=n)\
        coherence = np.clip(rng.normal(0.7, 0.12, size=n), 0, 1)\
        entropy = np.clip(rng.normal(0.28, 0.10, size=n), 0, 1)\
        shock_idx = rng.choice(n, size=max(1, n // 8), replace=False)\
        entropy[shock_idx] = np.clip(entropy[shock_idx] + rng.uniform(0.4, 0.7, size=len(shock_idx)), 0, 1)\
        coherence[shock_idx] = np.clip(coherence[shock_idx] - rng.uniform(0.2, 0.5, size=len(shock_idx)), 0, 1)\
\
    else:\
        work = rng.uniform(0.6, 1.2, size=n)\
        coherence = rng.uniform(0.2, 0.95, size=n)\
        entropy = rng.uniform(0.05, 0.9, size=n)\
\
    df = pd.DataFrame(\{\
        "t": t,\
        "work": work,\
        "coherence": coherence,\
        "entropy": entropy\
    \})\
    return df\
\
# -----------------------------\
# UI\
# -----------------------------\
st.title("Trust-as-Capacity Demo (VANU)")\
st.caption("A minimal demo of coherence-gated, entropy-discounted accumulation \'97 showing why trust is not a linear reputation score.")\
\
with st.sidebar:\
    st.header("Model parameters")\
\
    c_min = st.slider("Coherence threshold  C_min", 0.0, 1.0, 0.55, 0.01)\
    k = st.slider("Nonlinearity exponent  k  (coherence amplification)", 1.0, 6.0, 2.4, 0.1)\
    lam = st.slider("Entropy penalty  \uc0\u955 ", 0.0, 6.0, 2.0, 0.1)\
\
    st.divider()\
    st.header("Data")\
    mode = st.selectbox("Sample scenario", [\
        "Coherent builder",\
        "Noisy (engagement-like)",\
        "Mixed with shocks",\
        "Random"\
    ])\
    n = st.slider("Number of events", 10, 200, 60, 1)\
    seed = st.number_input("Random seed", min_value=0, max_value=10_000, value=7, step=1)\
\
    uploaded = st.file_uploader("\'85or upload CSV (columns: t, work, coherence, entropy)", type=["csv"])\
\
# Load data\
if uploaded is not None:\
    df = pd.read_csv(uploaded)\
    missing = [c for c in ["t", "work", "coherence", "entropy"] if c not in df.columns]\
    if missing:\
        st.error(f"CSV missing columns: \{missing\}. Expected: t, work, coherence, entropy")\
        st.stop()\
    df = df.sort_values("t").reset_index(drop=True)\
else:\
    df = generate_sample(n=n, mode=mode, seed=int(seed))\
\
# Compute VANU per event\
df["delta_vanu"] = [\
    vanu_delta(w, c, s, c_min=c_min, k=k, lam=lam)\
    for w, c, s in zip(df["work"], df["coherence"], df["entropy"])\
]\
df["vanu"] = df["delta_vanu"].cumsum()\
\
# PTA band per event (illustrative)\
df["pta_band"] = [pta_band(c, s) for c, s in zip(df["coherence"], df["entropy"])]\
\
# Summary metrics\
total_vanu = float(df["vanu"].iloc[-1]) if len(df) else 0.0\
earned_events = int((df["delta_vanu"] > 0).sum())\
earned_pct = earned_events / len(df) * 100 if len(df) else 0.0\
avg_coh = float(df["coherence"].mean())\
avg_ent = float(df["entropy"].mean())\
\
# -----------------------------\
# Layout\
# -----------------------------\
colA, colB, colC, colD = st.columns(4)\
colA.metric("Total VANU", f"\{total_vanu:.3f\}")\
colB.metric("Events earning VANU", f"\{earned_events\}/\{len(df)\}", f"\{earned_pct:.1f\}%")\
colC.metric("Avg coherence", f"\{avg_coh:.2f\}")\
colD.metric("Avg entropy", f"\{avg_ent:.2f\}")\
\
left, right = st.columns([1.2, 1.0])\
\
with left:\
    st.subheader("Cumulative VANU (trust-capacity accumulation)")\
    st.line_chart(df.set_index("t")["vanu"])\
\
    st.subheader("Per-event contributions")\
    st.bar_chart(df.set_index("t")["delta_vanu"])\
\
with right:\
    st.subheader("Signals (coherence & entropy)")\
    st.line_chart(df.set_index("t")[["coherence", "entropy"]])\
\
    st.subheader("PTA band readout (illustrative)")\
    band_counts = df["pta_band"].value_counts().rename_axis("PTA band").reset_index(name="count")\
    st.dataframe(band_counts, use_container_width=True, hide_index=True)\
\
st.subheader("Event table (what the kernel would see)")\
st.dataframe(df[["t", "work", "coherence", "entropy", "delta_vanu", "vanu", "pta_band"]], use_container_width=True)\
\
st.markdown(\
    """\
**How to narrate this in a screencast:**  \
- \'93Coherence below threshold earns nothing.\'94  \
- \'93Above threshold, coherence compounds nonlinearly (C^k).\'94  \
- \'93Entropy reduces the realized value (e^\{-\uc0\u955 S\}).\'94  \
- \'93So volume alone can\'92t game it \'97 only coherent, low-entropy contribution accumulates.\'94\
"""\
)\
}