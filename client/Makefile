CXXFLAGS=-Wall -O3 -I../common -I.
LIB_OBJECTS=udp-flaschen-taschen.o bdf-font.o graphics.o
LIB_CXXFLAGS=$(CXXFLAGS) -fPIC

LDFLAGS=-L. -lftclient

MAGICK_CXXFLAGS=`GraphicsMagick++-config --cppflags --cxxflags`
MAGICK_LDFLAGS=`GraphicsMagick++-config --ldflags --libs`

FFMPEG_LDFLAGS=`pkg-config --cflags --libs  libavcodec libavformat libswscale libavutil`

all : simple-example simple-animation send-text pong-game game-client

simple-animation: simple-animation.cc
simple-example: simple-example.cc
send-text: send-text.cc
game-client: game-client.cc
burn-in: burn-in.cc

pong-game: pong-game.cc game-engine.cc libftclient.a
	$(CXX) $(CXXFLAGS) -o $@ $^ $(LDFLAGS)

send-image : send-image.cc libftclient.a
	$(CXX) $(CXXFLAGS) $(MAGICK_CXXFLAGS) -o $@ $< $(MAGICK_LDFLAGS) $(LDFLAGS)

send-video: send-video.cc libftclient.a
	$(CXX) $(CXXFLAGS) -o $@ $< $(FFMPEG_LDFLAGS) $(LDFLAGS)

% : %.cc libftclient.a
	$(CXX) $(CXXFLAGS) -o $@ $< $(LDFLAGS)

%.o : %.cc
	$(CXX) $(LIB_CXXFLAGS) -c -o $@ $<

libftclient.a: $(LIB_OBJECTS)
	ar rcs $@ $^

clean:
	rm -f send-text send-image send-video simple-example simple-animation pong-game game-client $(LIB_OBJECTS) libftclient.a
