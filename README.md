# Python-Project
import hashlib
import heapq
from collections import defaultdict

# Data structures
class TreeNode:
    def __init__(self, patient_id, patient_data):
        self.patient_id = patient_id
        self.patient_data = patient_data
        self.left = None
        self.right = None

class PatientRecords:
    def __init__(self):
        self.root = None

    def insert(self, patient_id, patient_data):
        if not self.root:
            self.root = TreeNode(patient_id, patient_data)
        else:
            self._insert(self.root, patient_id, patient_data)
    
    def _insert(self, node, patient_id, patient_data):
        if patient_id < node.patient_id:
            if node.left:
                self._insert(node.left, patient_id, patient_data)
            else:
                node.left = TreeNode(patient_id, patient_data)
        else:
            if node.right:
                self._insert(node.right, patient_id, patient_data)
            else:
                node.right = TreeNode(patient_id, patient_data)
    
    def search(self, patient_id):
        return self._search(self.root, patient_id)
    
    def _search(self, node, patient_id):
        if not node or node.patient_id == patient_id:
            return node
        elif patient_id < node.patient_id:
            return self._search(node.left, patient_id)
        else:
            return self._search(node.right, patient_id)

class DoctorAppointments:
    def __init__(self):
        self.appointments = []

    def schedule(self, doctor_id, patient_id, appointment_time):
        heapq.heappush(self.appointments, (appointment_time, doctor_id, patient_id))

    def get_appointments(self):
        return [heapq.heappop(self.appointments) for _ in range(len(self.appointments))]

class MedicalInventory:
    def __init__(self):
        self.inventory = defaultdict(int)

    def add_item(self, item_name, quantity):
        self.inventory[item_name] += quantity

    def remove_item(self, item_name, quantity):
        if self.inventory[item_name] >= quantity:
            self.inventory[item_name] -= quantity
        if self.inventory[item_name] == 0:
            del self.inventory[item_name]
    
    def check_inventory(self, item_name):
        return self.inventory[item_name]

    def generate_alerts(self, threshold):
        return {item: qty for item, qty in self.inventory.items() if qty <= threshold}

# Sorting and Searching Algorithms
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quick_sort(left) + middle + quick_sort(right)

def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

# Security
class Security:
    def __init__(self):
        self.users = {}

    def hash_password(self, password):
        return hashlib.sha256(password.encode()).hexdigest()

    def add_user(self, username, password):
        self.users[username] = self.hash_password(password)

    def authenticate(self, username, password):
        hashed = self.hash_password(password)
        return self.users.get(username) == hashed

# Example usage
if __name__ == "__main__":
    # Patient records
    records = PatientRecords()
    records.insert(1, {"name": "John Doe", "age": 30, "condition": "Flu"})
    records.insert(2, {"name": "Jane Smith", "age": 25, "condition": "Cold"})

    print(records.search(1).patient_data)

    # Doctor appointments
    appointments = DoctorAppointments()
    appointments.schedule("Dr. Adams", 1, "2024-08-01 10:00")
    appointments.schedule("Dr. Brown", 2, "2024-08-01 11:00")

    print(appointments.get_appointments())

    # Medical inventory
    inventory = MedicalInventory()
    inventory.add_item("Aspirin", 100)
    inventory.add_item("Ibuprofen", 50)
    inventory.remove_item("Aspirin", 10)

    print(inventory.check_inventory("Aspirin"))
    print(inventory.generate_alerts(20))

    # Sorting and searching
    items = [5, 3, 8, 1, 2, 7]
    sorted_items = quick_sort(items)
    print(sorted_items)
    print(binary_search(sorted_items, 7))

    # Security
    security = Security()
    security.add_user("admin", "password123")
    print(security.authenticate("admin", "password123"))

    
    # Output
    
![pythonprojectss](https://github.com/user-attachments/assets/b94422c3-4904-40d0-8ccc-8f86b789ba95)
