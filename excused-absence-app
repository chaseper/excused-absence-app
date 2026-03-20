import streamlit as st
import json
from pathlib import Path
from datetime import datetime
import uuid

st.set_page_config(page_title="Absence App")

if "page" not in st.session_state:
    st.session_state.page = "dashboard"
Data_file = Path("requests.json")
def load_data():
    if Data_file.exists():
        with open(DATA_FILE, "r") as f:
            return json.load(f)
    return []

def save_data(data):
    with open(Data_file, "w") as f:
        json.dump(data, f)

requests = load_data()
st.sidebar.title("Menu")
if st.sidebar.button("Dashboard"):
    st.session_state.page = "dashboard"
    st.rerun()

if st.sidebar.button("Request"):
    st.session_state.page = "request"
    st.rerun()

if st.session_state.page == "dashboard":
    st.title("Dashboard")

    if len(requests) == 0:
        st.write("No data")
    else:
        event = st.dataframe(
            requests,
            on_select="rerun",
            selection_mode="single-row"
        )

        if event.selection.rows:
            i = event.selection.rows[0]
            st.write(requests[])

elif st.session_state.page == "request":
    st.title("Submit Request")

    with st.form("form"):
        email = st.text_input("Email")
        date = st.date_input("Date")
        date_str = date.strftime

        excuse = st.selectbox("Type", ["Medical", "University Competitions", "Other"])
        reason = st.text_area("Reason")
        note = st.text_area("Instructor Note")

        submit = st.form_submit_button("Submit")

        if submit:
            new = {
                "request_id": str(uuid.uuid4())[:8],
                "status": "Pending",
                "course_id": "011101",
                "student_email": email,
                "absence_date": date_str,
                "submitted_timestamp": datetime.now().strftime,
                "excuse_type": excuse,
                "explanation": reason,
                "instructor_note": note
            }

            requests.append(new)
            save_data(requests)

            st.success("Submitted")
            st.session_state.page = "dashboard"
            st.rerun()
