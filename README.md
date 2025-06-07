# EXP-5-A-
import heapq

def a_star(start, goal, get_neighbors, heuristic):
    open_set = []
    heapq.heappush(open_set, (0, start))
    came_from = {}
    g_score = {start: 0}

   while open_set:
        _, current = heapq.heappop(open_set)

   if current == goal:
            return reconstruct_path(came_from, current)

   for neighbor in get_neighbors(current):
            tentative_g_score = g_score[current] + 1  # Assume cost = 1

   if neighbor not in g_score or tentative_g_score < g_score[neighbor]:
                came_from[neighbor] = current
                g_score[neighbor] = tentative_g_score
                f_score = tentative_g_score + heuristic(neighbor, goal)
                heapq.heappush(open_set, (f_score, neighbor))

  return None  # No path found

def reconstruct_path(came_from, current):
    path = [current]
    while current in came_from:
        current = came_from[current]
        path.append(current)
    return path[::-1]

