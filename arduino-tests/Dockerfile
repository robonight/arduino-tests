FROM dockcross/base:latest

RUN git clone https://github.com/ikeyasu/arduino-mock.git /opt/arduino && cd /opt/arduino && git submodule update --init --recursive && rm -rf test && rm -f CMakeLists.txt
WORKDIR "/opt/arduino"
COPY "CMakeLists.1.txt" /opt/arduino/CMakeLists.txt

RUN mkdir /arduino
VOLUME [ "/arduino/project" ]

RUN touch touch.txt 
# change only behind this point
COPY "run.sh" /opt/arduino
COPY "CMakeLists.txt" /arduino

ENTRYPOINT [ "./run.sh" ]