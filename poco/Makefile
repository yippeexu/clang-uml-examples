CLANG_UML_BINARY ?= ../../clang-uml/debug/src/clang-uml

.PHONY: clean build diagrams plantuml

all: plantuml

poco:
		git clone https://github.com/pocoproject/poco && \
		cd poco && \
		git checkout poco-1.12.3

build: poco
		cd poco && \
		mkdir -p _build && \
		cd _build && \
		cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=ON ..

diagrams: build
		cd poco && \
		cp ../.clang-uml .clang-uml && \
		../$(CLANG_UML_BINARY) --query-driver .

plantuml: diagrams
		plantuml -tsvg puml/*.puml
		python3 ../generate_readme.py poco
		markdown-toc  --bullets "*" -i README.md

clean:
		rm -rf poco
