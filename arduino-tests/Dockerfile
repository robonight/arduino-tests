FROM dockcross/base:latest

RUN git clone https://github.com/ikeyasu/arduino-mock.git /arduino/mock && cd /arduino/mock && git submodule update --init --recursive && rm -rf test && rm -f CMakeLists.txt
WORKDIR "/arduino/mock"
COPY "CMakeLists.1.txt" /arduino/mock/CMakeLists.txt

VOLUME [ "/arduino/project" ]

RUN touch touch.txt 
# change only behind this point
COPY "run.sh" /arduino/mock
COPY "CMakeLists.txt" /arduino

ENTRYPOINT [ "./run.sh" ]