class Node:
    def __init__(self, word, word_type, meanings, examples):
        self.word = word
        self.word_type = word_type
        self.meanings = meanings
        self.examples = examples
        self.left = None
        self.right = None

class DictionaryBST:
    def __init__(self):
        self.root = None

    def insert(self, word, word_type, meanings, examples):
        if not self.root:
            self.root = Node(word, word_type, meanings, examples)
        else:
            self._insert_recursive(self.root, word, word_type, meanings, examples)

    def _insert_recursive(self, node, word, word_type, meanings, examples):
        if word < node.word:
            if node.left is None:
                node.left = Node(word, word_type, meanings, examples)
            else:
                self._insert_recursive(node.left, word, word_type, meanings, examples)
        elif word > node.word:
            if node.right is None:
                node.right = Node(word, word_type, meanings, examples)
            else:
                self._insert_recursive(node.right, word, word_type, meanings, examples)
        else:  # Update meanings and examples if word already exists
            node.meanings.extend(meanings)
            node.examples.extend(examples)

    def remove(self, word):
        self.root = self._remove_recursive(self.root, word)

    def _remove_recursive(self, node, word):
        if node is None:
            return node
        if word < node.word:
            node.left = self._remove_recursive(node.left, word)
        elif word > node.word:
            node.right = self._remove_recursive(node.right, word)
        else:
            if not node.left and not node.right:
                return None
            elif not node.left:
                return node.right
            elif not node.right:
                return node.left
            else:
                successor = self._find_min(node.right)
                node.word = successor.word
                node.word_type = successor.word_type
                node.meanings = successor.meanings
                node.examples = successor.examples
                node.right = self._remove_recursive(node.right, successor.word)
        return node

    def _find_min(self, node):
        while node.left:
            node = node.left
        return node

    def search(self, word):
        return self._search_recursive(self.root, word)

    def _search_recursive(self, node, word):
        if node is None or node.word == word:
            return node
        if word < node.word:
            return self._search_recursive(node.left, word)
        return self._search_recursive(node.right, word)

    def save_to_file(self, filename):
    # Use 'utf-8' encoding when writing to the file
        with open(filename, 'w', encoding='utf-8') as f:
            self._save_to_file_recursive(self.root, f)

    def _save_to_file_recursive(self, node, f):
        if node:
            f.write(f"{node.word} | {node.word_type} | {', '.join(node.meanings)} | {', '.join(node.examples)}\n")
            self._save_to_file_recursive(node.left, f)
            self._save_to_file_recursive(node.right, f)

    def load_from_file(self, filename):
    # Use 'utf-8' encoding when reading from the file
        with open(filename, 'r', encoding='utf-8') as f:
            for line in f:
                parts = line.strip().split(' | ')
                if len(parts) < 4:
                    continue  # skip any malformed lines
                word, word_type, meanings, examples = parts
                meanings_list = meanings.split(', ')
                examples_list = examples.split(', ')
                self.insert(word, word_type, meanings_list, examples_list)


def display_menu():
    print("----- Menu -----")
    print("1. Thêm từ mới")
    print("2. Xóa từ")
    print("3. Tra từ điển")
    print("4. Lưu từ điển vào tập tin")
    print("5. Nạp từ điển từ tập tin")
    print("6. Kết thúc")

def main():
    dictionary = DictionaryBST()

    while True:
        display_menu()
        choice = input("Chọn chức năng (1-6): ")

        if choice == '1':
            word = input("Nhập từ mới: ")
            word_type = input("Nhập loại từ (danh từ, động từ, ...): ")
            meanings = input("Nhập nghĩa của từ, phân tách bởi dấu phẩy: ").split(',')
            examples = input("Nhập ví dụ cho từ, phân tách bởi dấu phẩy: ").split(',')
            dictionary.insert(word.strip(), word_type.strip(), [meaning.strip() for meaning in meanings], [example.strip() for example in examples])
            print("Từ mới đã được thêm vào từ điển.")
        elif choice == '2':
            word = input("Nhập từ cần xóa: ")
            dictionary.remove(word.strip())
            print("Từ đã được xóa khỏi từ điển.")
        elif choice == '3':
            word = input("Nhập từ cần tra: ")
            node = dictionary.search(word.strip())
            if node:
                print(f"{node.word} ({node.word_type}): {', '.join(node.meanings)}")
                for example in node.examples:
                    print(f"Ví dụ: {example}")
            else:
                print("Từ không tồn tại trong từ điển.")
        elif choice == '4':
            filename = input("Nhập tên tập tin để lưu từ điển: ")
            dictionary.save_to_file(filename.strip())
            print("Từ điển đã được lưu vào tập tin.")
        elif choice == '5':
            filename = input("Nhập tên tập tin để nạp từ điển: ")
            dictionary.load_from_file(filename.strip())
            print("Từ điển đã được nạp từ tập tin.")
        elif choice == '6':
            print("Kết thúc chương trình.")
            break
        else:
            print("Chức năng không hợp lệ. Vui lòng chọn lại.")

if __name__ == "__main__":
    main()