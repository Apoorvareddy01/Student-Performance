import streamlit as st
import pandas as pd
 
st.set_page_config(page_title="Student Case Study", page_icon="🎓", layout="wide")

# Sample Data
data = pd.DataFrame({
    "Name": ["Amit", "Priya", "Rahul", "Sneha", "Kiran"],
    "Maths": [88, 92, 80, 70, 95],
    "Science": [90, 85, 78, 92, 88],
    "English": [75, 80, 85, 70, 90]
})

# 🏫 Title with style
st.markdown("<h1 style='color:#4CAF50; text-align:center;'>📊 Student Performance Dashboard</h1>", unsafe_allow_html=True)

# Add filters sidebar
st.sidebar.header("🔍 Filters")

# Filter by student name
selected_students = st.sidebar.multiselect(
    "Select Students", options=data["Name"], default=data["Name"]
)

# Filter by subject
selected_subjects = st.sidebar.multiselect(
    "Select Subjects", options=["Maths", "Science", "English"], default=["Maths", "Science", "English"]
)

# Filter by minimum average score
min_avg = st.sidebar.slider("Minimum Average Score", 0, 100, 0)


# Show raw data
st.subheader("Dataset")
st.dataframe(data, use_container_width=True)

# Show summary
st.subheader("Summary Statistics")
st.write(data.describe(), use_container_width=True)

# Add new columns
data["Total"] = data[["Maths", "Science", "English"]].sum(axis=1)
data["Average"] = data["Total"] / 3

# Find toppers
top_student = data.loc[data["Total"].idxmax(), "Name"]
math_top = data.loc[data["Maths"].idxmax(), "Name"]
science_top = data.loc[data["Science"].idxmax(), "Name"]
english_top = data.loc[data["English"].idxmax(), "Name"]

# Show results
st.subheader("Case Study Results")
st.dataframe(data)

st.success(f"🏆 Overall Top Performer: **{top_student}**")
st.info(f"📘 Best in Maths: **{math_top}**")
st.info(f"🔬 Best in Science: **{science_top}**")
st.info(f"✍️ Best in English: **{english_top}**")
    its a student performance dashboard  using streamlit it used to bulid interactive dashboard/app.
# Optional chart
st.subheader("Performance Visualization")
st.bar_chart(data.set_index("Name")[["Maths", "Science", "English"]])
